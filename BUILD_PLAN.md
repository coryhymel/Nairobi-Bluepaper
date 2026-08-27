# Build Plan — Interactive Findings Page
## "Measuring Knowledge Gains from Structured Training in AI-Assisted Software Engineering"

**Deliverable:** a single standalone `index.html` in this folder — a public-facing interactive summary of the whitepaper.
**Audience:** engineering and L&D leaders deciding whether structured agentic-tooling training is worth funding.
**Author attribution:** Cory Hymel · Andela Research.
**Executor:** Claude Code. Read this document end to end before writing any code.

---

## 1. Objective and success criteria

The page must accomplish four things, in priority order:

1. **Land one argument:** access to a coding agent and proficiency with one are not the same thing, and two weeks of structure measurably closed part of that gap.
2. **Let the reader test themselves** against the same 12-item assessment the cohort took, and see where they land relative to the 41 participants.
3. **Stay scientifically honest** — no control group, identical pre/post instrument, ceiling effects, exploratory framing — without becoming unreadable.
4. **Look like it belongs to the same research series** as `Emergent-Role-Research-Findings/index.html`.

**Done when:**
- Single `index.html` opens correctly from `file://` with no network access and no console errors.
- Every number on the page reconciles to the whitepaper or to a documented derivation from the participant data (see §5.4).
- The assessment is completable start-to-finish on a 375px-wide viewport.
- All 13 sections present, all 5 interactives functional, keyboard-navigable, and `prefers-reduced-motion` respected.

---

## 2. Inputs

| File | Status | Use |
|:---|:---|:---|
| `Can-Short-Structured-Training-Improve-Applied-Agentic-Engineering-Knowledge.md` | ✅ in folder | Source of all statistics, framing, limitations, references |
| `Pre_Post Survey Questions.md` | ✅ in folder | Full text of all 12 items: stems, four options each, correct answer, and the *Principle* explainer line |
| `../Emergent-Role-Research-Findings/index.html` | ✅ available (parent dir) | **Design system source.** Lift the `:root` token block, component CSS, and the base64 Andela logo verbatim |
| Participant-level pre/post data | ⚠️ **NOT YET IN FOLDER** | Required for Phase 2. See §5.1 for the expected contract |

**Blocking prerequisite.** Cory has confirmed participant-level data exists but it is not in this folder. Before starting Phase 2, expect a file such as `participants.csv` or an export from the assessment platform. If it has not arrived when you reach Phase 2, build the aggregate-only fallback described in §5.5 and leave the participant-level code paths stubbed behind a single feature flag — do **not** invent participant records.

---

## 3. Hard constraints

- **Single file.** One `index.html`. All CSS and JS inline. No build step, no bundler, no separate assets.
- **Zero external requests.** No CDN, no D3, no analytics, no remote fonts. Google Fonts are used by the reference page; here, inline a `@font-face`-free fallback stack instead — see §4.2. Every chart in this page is bars, dumbbells, slopes, and a dot grid, all of which are straightforward hand-rolled SVG. Do not add a charting library.
- **No PII, ever.** Participant data will contain email addresses (the paper states pairing was done on normalized emails). Strip every identifier during preprocessing. Participants appear in the shipped file only as `p01`…`p41`. No emails, names, employers, or free-text responses in the HTML. This is non-negotiable and must be verified in §11.
- **No fabricated data.** If a number cannot be derived from the whitepaper or the participant file, it does not appear on the page. Approximations must be visibly labeled as such.
- **Print-tolerable.** A `@media print` block that hides the interactives and nav and renders the prose and charts cleanly. Low effort, high perceived quality.

---

## 4. Design system

### 4.1 Tokens — copy this block verbatim from the reference page

```css
:root{
  --darker-kale:#10292C; --emerald:#338632; --dark-green-black:#424D53;
  --lighter-green-black:#E7E9EA; --lightest-green-black:#F5F5F5;
  --almost-white:#FAFAFA; --white:#FFFFFF;
  --dark-kale:#1F3A3D; --teal:#307C84; --light-emerald:#7FC87C;
  --lighter-emerald:#D9EED8; --lightest-emerald:#ECF7EC;
  --light-kale:#7CBFC7; --lighter-kale:#E0F3F5; --lightest-kale:#F0FAFB;
  --opal:#B0D6CE; --light-opal:#E7F2F0;
  --ink:#10292C; --body:#424D53; --line:#E7E9EA; --accent:#338632;
  --serif:'Droid Serif',Georgia,'Times New Roman',serif;
  --sans:'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;
  --maxw:1180px;
}
```

**Add these page-specific semantic tokens.** This page needs a "got worse" color, which the reference did not:

```css
:root{
  --gain:#338632;        /* improvement — emerald */
  --gain-soft:#D9EED8;   /* improvement fill */
  --loss:#B4531F;        /* decline — burnt sienna, on-brand-adjacent, not alarm red */
  --loss-soft:#F4E3DA;
  --flat:#9DBAB3;        /* no change */
  --pre:#B0D6CE;         /* pre-program state — opal */
  --post:#338632;        /* post-program state — emerald */
  --you:#1F3A3D;         /* the reader's own marker — dark kale */
}
```

Rationale for `--loss`: a true red would read as "error" and overstate three declines that are partly measurement noise. Burnt sienna reads as "moved the wrong way" without alarm.

### 4.2 Type

Serif (`--serif`) for the hero headline, every `h2.head`, and all large statistics. Inter/system sans for everything else. Body 17px / 1.65.

The reference loads Inter and Droid Serif from Google Fonts. Because this page must work offline, **drop the `<link>` tags and rely on the fallback stacks already declared in the tokens** (Georgia for serif, system UI for sans). Georgia is a close enough tonal match to Droid Serif that the family resemblance holds. If Cory later wants exact typographic parity, fonts can be base64-inlined as a follow-up — note it in the reproducibility block, do not do it now.

### 4.3 Components to inherit verbatim

Pull these from the reference page's `<style>` block, unchanged unless noted:

`.masthead` (sticky, blurred) · `.brand` · `.topnav` · `.hero` + `.spark-field` SVG pattern · `.statstrip` / `.stat` · `section` padding rhythm · `.section-alt` / `.section-tint` / `.section-dark` · `.eyebrow` / `.kicker` · `h2.head` · `.lead` / `.narrow` / `.muted` · `.pull` (pull quote) · `.findgrid` / `.find` / `.fnum` (numbered findings) · `.stepper` / `.step` · `.figure` / `.figtitle` / `.figsub` / `.cap` · `.valgrid` / `.valcard` / `.vn` / `.vl` · `.limits` / `.lim` · `.closing` / `.repro` · `.foot` · `.fade` scroll-reveal · `.tablewrap` + sortable table styles · `.gtip` tooltip

Also lift the inline base64 Andela logo `<img>` from both the masthead and the footer.

### 4.4 New components to build

| Component | Purpose |
|:---|:---|
| `.guess` | Guess-the-gain drag widget (§7.1) |
| `.quiz` | Assessment engine shell: card, progress, options, feedback panel, results (§7.2) |
| `.dumbbell` | Item-level pre→post chart (§7.3) |
| `.dotmatrix` | 12 × 41 person-item transition grid (§7.4) |
| `.slopes` | Baseline-group slope chart with ceiling overlay (§7.5) |
| `.demo` | Scripted terminal micro-demo (§8) |
| `.stat-sub` | Small secondary line under a plain-English claim, holding the formal statistics. Used ~15 times. `font-size:13px; color:#6c7a76; font-variant-numeric:tabular-nums;` |

### 4.5 The tone rule — enforce this everywhere

**Every primary sentence is plain English. Every statistic lives in a `.stat-sub` line beneath it.**

> Scores rose about twelve points on average.
> <span class="stat-sub">+11.6 percentage points · 95% CI [6.4, 16.8] · *p* < .001 · Cohen's *d*z = 0.70 · *n* = 41 paired</span>

This preserves full scientific credibility while never blocking the read. If a sentence contains a parenthetical statistic, it is wrong — move it down.

---

## 5. Data layer

All data lives in JS `const` declarations at the top of a single `<script>` block, in the shape below. Generate these from the sources; do not hand-transcribe the item text (copy it programmatically or with great care from `Pre_Post Survey Questions.md`).

### 5.1 Expected participant data contract

Whatever arrives, normalize to this. One row per participant per item, plus a per-participant summary:

```js
// Anonymized. NO emails, names, or identifiers.
const PARTICIPANTS = [
  { id:'p01', pre:5, post:9, group:'low',  timePre:22.4, timePost:9.1,
    items:[ /* 12 entries */ {q:1, pre:true, post:true}, ... ] },
  ...
]; // length 41
```

`group` is derived, not supplied: `pre <= 6 → 'low'`, `pre 7-8 → 'mid'`, `pre >= 9 → 'high'`.

If the source export lacks per-item responses and has only totals, set `items:null` and the dot matrix falls back to the Appendix B aggregate construction (§5.5).

### 5.2 Item bank — the 12 assessment items

```js
const ITEMS = [
  { q:1,
    concept:'Context as the bottleneck',
    stem:'A developer has carefully reworded the same prompt four times...',
    options:['The model version being used lacks...', '...', '...', '...'],
    correct:3,               // zero-indexed: D
    principle:'Instead of a perfect prompt, build perfect context...',
    pre:90.2, post:92.7,     // % correct, from Appendix A
    trans:{wc:4, cw:3, sc:34, sw:0}  // Appendix B
  },
  ...
];
```

Correct-answer key, zero-indexed, verified against `Pre_Post Survey Questions.md`:

| Q | Concept | Correct | Pre % | Post % | Δ |
|:--|:--|:--:|--:|--:|--:|
| 1 | Context as the bottleneck | 3 (D) | 90.2 | 92.7 | +2.4 |
| 2 | Verification criteria ("Done When") | 3 (D) | 61.0 | 87.8 | **+26.8** |
| 3 | Repository-guidance hygiene (AGENTS.md) | 1 (B) | 58.5 | 90.2 | **+31.7** |
| 4 | Team defaults (MCP / skill / automation) | 0 (A) | 73.2 | 87.8 | +14.6 |
| 5 | Sandbox and network constraints | 2 (C) | 51.2 | 90.2 | **+39.0** |
| 6 | Specialized agent roles | 1 (B) | 58.5 | 70.7 | +12.2 |
| 7 | Agent-first operating model | 0 (A) | 97.6 | 100.0 | +2.4 |
| 8 | Planning artifacts for long tasks | 3 (D) | 80.5 | 90.2 | +9.8 |
| 9 | UI observation tools | 3 (D) | 97.6 | 92.7 | −4.9 |
| 10 | CI security-review integration (SDK) | 2 (C) | 46.3 | 41.5 | −4.9 |
| 11 | Worktrees for parallel agent work | 0 (A) | 70.7 | 87.8 | +17.1 |
| 12 | Durable source-of-truth context | 1 (B) | 43.9 | 36.6 | **−7.3** |

Appendix B transitions (wrong→correct, correct→wrong, stayed correct, stayed wrong):

```
Q1  4/3/34/0    Q2 13/2/23/3    Q3 13/0/24/4    Q4  8/2/28/3
Q5 18/2/19/2    Q6  8/3/21/9    Q7  1/0/40/0    Q8  5/1/32/3
Q9  0/2/38/1    Q10 4/6/13/18   Q11 8/1/28/4    Q12 4/7/11/19
```

### 5.3 Aggregate constants

```js
const SUMMARY = {
  nPaired:41,
  attempts:{ preTotal:82, preComplete:76, postTotal:47, postComplete:41 },
  meanCorrect:{ pre:8.29, post:9.68, delta:1.39 },
  meanPct:{ pre:69.1, post:80.7, deltaPp:11.6 },
  ci:[6.4, 16.8], p:'<.001', wilcoxonP:'<.0001', dz:0.70,
  medianCorrect:{ pre:8, post:10 },
  minCorrect:{ pre:4, post:6 },
  maxCorrect:{ pre:12, post:12 },
  medianMinutes:{ pre:18.5, post:8.7, delta:-9.8 },
  movement:{ improved:24, same:12, declined:5, improvedTwoPlus:16 },
  movementPct:{ improved:58.5, same:29.3, declined:12.2 },
  thresholds:{ atLeast9Pre:46.3, atLeast9Post:78.0, atMost7Pre:15, atMost7Post:4 },
  fasterPost:36, fasterPostPct:87.8
};

const BASELINE = [
  { key:'low',  label:'Started with 6 or fewer correct',  n:11, pre:5.36,  post:8.82,  gain:3.45 },
  { key:'mid',  label:'Started with 7 or 8 correct',      n:11, pre:7.64,  post:9.27,  gain:1.64 },
  { key:'high', label:'Started with 9 or more correct',   n:19, pre:10.37, post:10.42, gain:0.05 }
];

const MODULES = [
  { name:'Module 1 · Foundations', items:10, learners:58, attempts:69, passRate:100,
    avgScore:87, itemCorrect:87.4, attemptsPerLearner:1.2, firstAttemptPass:86,
    additionalAttempts:11, additionalPerLearner:0.19, sdItemDifficulty:7.1,
    errorConcentration:'Three questions account for 50.6% of all errors' },
  { name:'Module 2 · Advanced Workflows', items:10, learners:54, attempts:76, passRate:100,
    avgScore:82, itemCorrect:82.1, attemptsPerLearner:1.4, firstAttemptPass:72,
    additionalAttempts:22, additionalPerLearner:0.41, sdItemDifficulty:11.0,
    errorConcentration:'Four questions account for 66.2% of all errors' }
];
```

### 5.4 Reconciliation — a required verification step

Write a short throwaway script (Node or Python, **not** shipped in the HTML) that loads the participant data and asserts it reproduces the published marginals. Every one of these must pass before the participant data is used on the page:

- `PARTICIPANTS.length === 41`
- `mean(pre) ≈ 8.29` and `mean(post) ≈ 9.68` (±0.01)
- `median(pre) === 8`, `median(post) === 10`
- `min(pre) === 4`, `min(post) === 6`, `max(pre) === 12`, `max(post) === 12`
- count improved `=== 24`, unchanged `=== 12`, declined `=== 5`
- no participant declines by more than 1 item
- count gaining ≥2 `=== 16`
- share scoring ≥9: pre `≈ 46.3%` (19/41), post `≈ 78.0%` (32/41)
- count scoring ≤7: pre `=== 15`, post `=== 4`
- baseline group sizes `=== 11 / 11 / 19` and group means match Table 2 (±0.01)
- if per-item data present: each item's four transition counts match Appendix B exactly, and each item's pre/post correct % matches Appendix A (±0.1)

**If any assertion fails, stop and report the discrepancy to Cory.** Do not adjust the data to fit, and do not silently ship a mismatch. A failed assertion means either the export differs from the analysis run or the paper has an error — both need a human decision.

### 5.5 Aggregate-only fallback

If participant data does not arrive, or arrives without per-item detail:

- **Score distribution** (for the quiz comparison): construct pre and post histograms only from what is published — mean, median, min, max, and the ≥9 / ≤7 threshold counts. Render as a **coarse banded distribution, not 41 individual dots**, and caption it: *"Distribution shape reconstructed from published summary statistics; individual participant scores not shown."* Never draw 41 dots you cannot place.
- **Dot matrix:** fully buildable from Appendix B without participant data — each row's 41 dots are the four transition counts laid out in fixed order (stayed correct → improved → declined → stayed wrong). Caption it: *"Dots are ordered by outcome, not by participant; the page does not claim to show which individual moved where."*
- Set `const HAS_PARTICIPANT_DATA = false;` and branch on it in one place. Keep the true-branch code written and ready.

---

## 6. Section-by-section specification

Thirteen sections plus masthead and footer, matching the reference page's density and rhythm.

### 0 · Masthead
Sticky. Andela logo (base64 from reference) · divider · `Research` tag. Right-side nav anchors: `Findings · Take the test · What moved · The program · Limits`. Hidden below 820px, as in the reference.

### 1 · Hero — `.hero`, dark kale
- Eyebrow: `Andela Research · Developer learning`
- H1 (serif, `clamp(2.6rem,6vw,4.6rem)`): **"Having the tool is not knowing how to use it"**
- Dek (~55 words): 41 professional engineers, two weeks of structured training on agentic coding workflows, the same 12-question scenario assessment before and after. What moved, what didn't, and what stayed stubbornly hard.
- Meta line 1: `A pre–post program evaluation of 41 professional developers · 2026`
- Meta line 2: `Author: Cory Hymel · Head of Research, Andela`
- Reuse the `.spark-field` SVG pattern at `opacity:.06`.

### 2 · Stat strip — `.statstrip`, dark kale, three stats
| `41` | `+11.6 pts` | `2 weeks` |
|:--|:--|:--|
| engineers assessed before and after | average gain on a 12-item scenario test | of structured instruction |

### 3 · Guess the gain — `.guess`, light
Full spec in §7.1. Opens with: *"Before we show you the result — what would you expect?"* This section deliberately sits **before** any finding, so the reader commits a prior.

### 4 · The question we asked — `#question`, white
Eyebrow `The question` → h2 `What we set out to test`.

Content beats:
- AI coding tools have become agents: they read repositories, edit files, run commands, call tools, and check their own work. That is a different skill from writing code.
- The skills that matter now sit around the agent, not in it — designing intent, exposing the right context, constraining what the agent may do, and defining what "done" means.
- Research consistently finds these habits are not absorbed automatically from tool access. Cite Vaithilingam 2022, Liang 2024, Perry 2023 (the security finding — developers with an assistant wrote less secure code *and* were more confident it was secure — is the single most persuasive citation for a leadership audience; give it its own sentence).
- Productivity evidence is genuinely mixed: Peng 2023 found 55.8% faster task completion; Becker 2025 found experienced developers 19% *slower* in mature repositories. Present this as a real tension, not a footnote.
- Pull quote (`.pull.serif`): **"Access to a coding agent and proficiency with one are not the same thing."**
- Close with the open question the study addresses: can experienced engineers pick up this operational knowledge from a short, structured program?

### 5 · Three findings at a glance — `.findgrid`, `.section-alt`
Reuse the reference's `01 / 02 / 03` numbered card layout exactly.

**01 — Two weeks moved the needle.** Average score went from about 69% to about 81%. Nearly three in five participants improved, and nobody dropped more than a single question. `.stat-sub`: *+11.6 pp · 95% CI [6.4, 16.8] · p < .001 · Wilcoxon p < .0001 · d_z = 0.70*

**02 — The people who knew least gained the most.** Participants who started with 6 or fewer correct gained about 3.5 questions. Those who started at 9 or above gained essentially nothing — though on a 12-question test they had almost no room left to move. Be explicit about the ceiling caveat *inside the card*; do not let this read as "training doesn't help seniors." `.stat-sub`: *+3.45 vs. +1.64 vs. +0.05 items · n = 11 / 11 / 19*

**03 — The gains were in operating mechanics, not big ideas.** The biggest jumps were practical: what the sandbox actually blocks (+39 points), keeping repository guidance lean (+31.7), and writing down what "done" means (+26.8). The strategic principle — humans steer, agents execute — was already understood by almost everyone before the program began. `.stat-sub`: *Q7, the agent-first operating model, was answered correctly by 97.6% before instruction and 100% after*

### 6 · Take the assessment — `#assessment`, `.section-tint` or dark
The anchor interactive. Full spec in §7.2. Give this section its own visual treatment so it reads as an application rather than an article — a bordered/tinted container, generous padding, and a clear "12 questions · about 10 minutes" affordance with the "quick 5" alternative.

### 7 · What moved — `#moved`, white
Two figures, each in a `.figure` wrapper with `.figtitle` / `.figsub` / `.cap`.

- **Figure 1 — item-level dumbbell** (§7.3). Figsub explains: each row is one question, the opal dot is before, the emerald dot is after, and the three sienna rows moved backwards.
- **Figure 2 — the 492-dot people matrix** (§7.4). Figsub explains that a net gain hides churn: on question 12, four people got it right who hadn't, and seven got it wrong who previously had.
- Between them, prose on the paper's real observation: strategic understanding and operational judgment develop at different rates. The reader who has just taken the test will feel this.

### 8 · The baseline paradox — `#baseline`, `.section-alt`
Slope chart (§7.5) plus the honest reading: the flat high-baseline line is at least as much a property of the instrument as of the learners. A 12-item test cannot measure advanced learning in someone who already scores 10.4. Explicitly state: *this result should not be read as "experienced engineers gained nothing."*

### 9 · Three questions that stayed hard — `#hard`, white
The most quotable section. **Get the framing precisely right — there are two overlapping groups and they must not be conflated:**

- **Still hardest after training** (lowest post-program correctness, and what the paper calls persistent difficulty): **Q12** durable source-of-truth (36.6%), **Q10** CI security-review integration (41.5%), **Q6** specialized agent roles (70.7%).
- **Actually got worse:** Q12 (−7.3), Q10 (−4.9), and Q9 (−4.9). Q9's decline is from 97.6% to 92.7% — ceiling noise on a question nearly everyone already answered correctly. Say so plainly and do not include Q9 in the "hard" narrative.

Render Q12, Q10, and Q6 as three inline playable cards (reuse the quiz engine's question component). Then the insight: all three ask the reader to pick between *adjacent plausible mechanisms* — an MCP connector versus a checked-in markdown file, the SDK versus a scheduled automation versus a skill. There is no wrong-sounding option to eliminate. Knowing the principle does not tell you which lever to pull. That is a genuinely useful observation about agentic tooling, and it is the sentence most likely to get quoted.

### 10 · Inside the program — `#program`, `.section-alt`
Method section, reusing `.stepper`. Steps: (1) two weeks, fully online · (2) asynchronous materials for self-study · (3) four one-hour live sessions, two per module, in a concept → demo → practice → support format · (4) Module 1: Codex foundations — setup, the agent loop, prompt and context design, planning, verification criteria, repository guidance · (5) Module 2: advanced workflows — configuration, permissions and sandboxing, skills, MCP, automations, memory, parallel work, code review, long-horizon execution · (6) a required 10-item quiz per module, retries allowed · (7) the post-program assessment, taken before capstone access.

Study-design facts stated plainly here: mid- to senior-level engineers based in Africa; limited or no prior Codex experience; some affiliated with Andela's talent network, some not; all used the Codex extension for VS Code. Pre-assessment 82 attempts / 76 completed; post 47 / 41; paired sample 41. *(Per Cory: cohort geography stated factually here, no dedicated module.)*

Host the two micro-demos (§8) in this section.

### 11 · Module 2 was harder — `#modules`, white, compact
Paired horizontal bars from `MODULES`. The punchy framing: both modules ended at a 100% pass rate because retries were allowed, so the pass rate says nothing. The retry count says everything — advanced workflows took **2.15× more additional attempts per learner** (0.41 vs. 0.19), and first-attempt pass fell from 86% to 72%. Note also that difficulty was concentrated: three questions caused half of Module 1's errors, four caused two-thirds of Module 2's.

### 12 · What this does not claim — `#limits`, `.section-alt`, `.limits` component
Six items, each `.lim` with dot + `h4` + paragraph:

1. **No control group.** The single largest limitation. Scores rose, but we cannot attribute the rise to the program with the confidence a controlled trial would give.
2. **The same test, twice.** Familiarity plausibly explains part of the speed gain, and may have primed attention to certain topics. Counterweight, stated fairly: participants received no scores and no answer feedback after the pre-test, so familiarity alone does not explain newly correct answers on previously missed items.
3. **The instrument was built for the curriculum.** Developed by Andela's internal Assessment Team and reviewed by subject-matter experts, but not an independently validated research scale.
4. **Twelve questions is a short ruler.** Little headroom for high scorers, which limits what the flat high-baseline result can mean.
5. **Knowledge, not performance.** The study measures what participants could recognize and select in scenarios. It does not measure whether they shipped better, safer, or faster code.
6. **Exploratory by construction.** The research question and statistical framing were developed after data collection. Read as program-evaluation evidence, not causal proof.

### 13 · Why it matters — `.section-dark.closing`
Andela framing, mirroring the reference page's closing register: skills-first reading of the market, tailoring learning programs, talent debt. Then the leadership takeaway: rolling out an agentic coding tool is a procurement decision; getting proficiency out of it is a learning decision, and the two are routinely confused.

Then a `.repro` block: paired *n* = 41 matched on normalized email addresses; identical 12-item multiple-choice instrument administered pre-program and immediately post-instruction; scored 0–12; paired *t*-test with Wilcoxon signed-rank robustness check; 95% CI [6.4, 16.8]; Cohen's *d*z = 0.70; baseline groups assigned post hoc and not prespecified; participant-level data anonymized before publication; body serif renders in Georgia where Droid Serif is unavailable.

Add a link to the full whitepaper.

### 14 · Footer
`.foot` — logo, `Andela Research · Developer learning · © 2026 Andela`.

---

## 7. Interaction specifications

### 7.1 Guess the gain — `.guess`

**Purpose:** make the reader commit a prior before the reveal, so the central number lands instead of washing over them.

**Behavior**
1. A horizontal scale, 0–100%, with the pre-program mean (69.1%) fixed and labeled `Before the program`.
2. A draggable handle labeled `Where do you think scores landed?`, initialized at 69.1% (no anchoring hint), constrained to 40–100%.
3. Full input parity: pointer drag, arrow keys (±1, Shift ±5), and a `range` input as the underlying control so it is native-accessible. Live `aria-valuetext` announcing the current guess.
4. On release/commit, a `Show me` button activates. On click:
   - The true post value (80.7%) animates in as a second marker over ~600ms.
   - Feedback text, chosen by `|guess − 80.7|`: within 2 pts → *"Almost exactly right."*; within 6 → *"Close."*; guess < 74.3 → *"You underestimated it."*; guess > 87.1 → *"You expected more than we found."*
   - `.stat-sub` reveals the formal result.
5. State is one-way — no reset. The reveal is the payload.
6. `prefers-reduced-motion`: no animation, immediate render.

**Mobile:** the range input handles touch natively. Ensure a ≥44px touch target.

### 7.2 The assessment engine — `.quiz`

The centerpiece. Build it as a small state machine, not a pile of DOM handlers.

**State**
```js
{ mode:'full'|'quick', idx:0, answers:Array(12).fill(null),
  startedAt:null, finishedAt:null, phase:'intro'|'question'|'feedback'|'results' }
```
`quick` mode uses the five highest-gain items: **Q5, Q3, Q2, Q11, Q4** (+39.0, +31.7, +26.8, +17.1, +14.6).

**Intro card**
Two buttons: `Take all 12 · about 10 minutes` and `Quick 5 · about 4 minutes`. One line setting expectations: these are the actual questions the cohort answered, scenario-based, one right answer each. Note that a timer runs, because time-to-complete is itself one of the findings.

**Question card**
- Progress: `Question 3 of 12` plus a thin emerald progress bar.
- Stem in serif at ~1.25rem. The stems are long — respect that with generous line height and a `max-width` around 62ch.
- Four options as large clickable cards (not radio dots): full-width, 1px `--line` border, 12px radius, hover lifts to `--lightest-emerald`. Keyboard: `1`–`4` and `A`–`D` select; `Enter` confirms; arrow keys move focus.
- Selecting does **not** auto-advance. A `Check answer` button confirms. This prevents mis-taps destroying the run.

**Feedback panel** — reveals in place beneath the options, three parts:
1. **Verdict.** Correct → emerald check, "Correct." Incorrect → sienna, "Not quite," with the correct option highlighted in emerald and the chosen one marked.
2. **The principle.** The `principle` string from `Pre_Post Survey Questions.md`, in a tinted callout. This is the highest-value content on the page — the reader learns something concrete on every single question.
3. **The cohort comparison.** Two small horizontal bars: `Participants before training — 51.2%` (opal) and `after training — 90.2%` (emerald). Plus one contextual sentence, branching on their answer:
   - Right, and it was a high-gain item → *"Half the cohort missed this before the program. Nine in ten got it after."*
   - Wrong, and post % is high → *"Nine in ten participants had this right by the end of the program."*
   - Wrong on Q10 or Q12 → *"You're in good company — this one got harder after training."*

Then `Next question` (or `See your results` on the last).

**Results card** — the payoff, four elements:
1. **Score**, large serif: `9 / 12` with the percentage beneath.
2. **Your position in the distribution.** A dot plot of the 41 participants' pre and post scores (two rows, 0–12 axis) with the reader's score dropped in as a `--you` marker spanning both rows. Caption: *"You scored 9. The cohort averaged 8.29 before the program and 9.68 after."* Add plain-English placement: above/at/below each mean. **Requires participant data; falls back per §5.5.**
3. **Your time.** `You: 6m 40s · Cohort median before: 18.5 min · after: 8.7 min`, with the honest caveat immediately adjacent: participants answered identical questions twice, so their speed-up cannot be separated from familiarity — and the reader saw feedback after every question, which they did not. Do not let this read as a fair comparison; say why it isn't.
4. **Your item card.** All 12 (or 5) items listed with your result, each expandable back to stem + principle. Plus a `Jump to the item chart` link — clicking scrolls to §7 with the reader's answers now overlaid (see 7.3).

Also: a copy-to-clipboard share line — `I scored 9/12 on the agentic engineering assessment from Andela's training study. The cohort averaged 8.3 before training, 9.7 after.` Clipboard only, no social intents, no tracking.

**Persistence:** write `{score, answers, mode, elapsedMs, ts}` to `localStorage` under `andela.agentic-quiz.v1`, wrapped in try/catch (private browsing throws). On revisit, the intro card offers `Resume` / `See your previous result` / `Start over`. Never let a storage failure break the page — if it throws, silently degrade to session-only.

**Accessibility:** the feedback panel is `aria-live="polite"`. Focus moves to the feedback heading on reveal and to the stem on advance. Full keyboard completability is a release requirement.

### 7.3 Item-level dumbbell — `.dumbbell`

Hand-rolled SVG, twelve rows.

- Y: the 12 items, labeled by concept (not "Q5" — "What the sandbox blocks"). X: 0–100% correct.
- Each row: an opal dot (pre) and an emerald dot (post) joined by a 3px connector. Connector emerald where post > pre, sienna where post < pre, `--flat` where equal.
- Value labels at each dot end; the delta right-aligned in a fixed column, tabular figures, `+39.0 pp` style.
- **Sort control:** `By gain` (default, descending) · `By question order` · `By final score`. Animate row reordering with a FLIP-style transform, disabled under `prefers-reduced-motion`.
- **Row click** expands an inline detail: full stem, four options with the correct one marked, and the principle. Reuse the quiz's question component read-only.
- **Reader overlay:** if quiz results exist in state or localStorage, each row gets a small `--you` glyph — a check or cross at the row's right edge — plus a legend entry `Your answer`. This is the moment the reader's data joins the study's data. Make sure it is unmistakable.
- Mobile: labels move above each row, chart scrolls horizontally inside `overflow-x:auto`.

### 7.4 The 492-dot people matrix — `.dotmatrix`

Twelve rows of 41 dots. Each dot is one participant on one question.

- Colors: stayed correct → `--gain-soft`; **improved (wrong→correct)** → `--gain` solid; **declined (correct→wrong)** → `--loss` solid; stayed wrong → `--flat` at 35% opacity.
- Ordering within a row: stayed-correct, improved, declined, stayed-wrong — so the solid emerald and sienna blocks sit adjacent in the middle and are instantly comparable across rows.
- Dots ~9px with 3px gaps; rows labeled by concept on the left.
- Hover/focus a row → tooltip (`.gtip`) with the four counts in plain words: *"13 people got this right who hadn't before. Nobody went the other way."*
- **Toggle:** `Who moved` (default) ↔ `Net change` (collapses each row to a single signed bar). Gives the skimmer a fast read and the curious reader the full picture.
- Caption must state whether dots represent identified participants or are outcome-ordered (§5.5).

Q3 (13 improved / 0 declined) and Q12 (4 improved / 7 declined) are the two rows that tell the story — the visual should make them pop without special-casing them.

### 7.5 Baseline slopes — `.slopes`

- Three lines, pre → post, on a shared 0–12 y-axis. Label each with group name, *n*, and gain.
- Low-baseline line in `--gain` at full weight; mid in `--teal`; high in `--flat` — visual hierarchy matching the argument.
- **Ceiling overlay toggle** (`Show remaining headroom`): shades the region between each group's post-score and the 12-point maximum. The high-baseline group's shaded band is visibly tiny — 1.58 points. This turns the paper's caveat into something the reader sees rather than reads. Make this toggle prominent; it is the honest heart of the section.

---

## 8. Micro-demos — `.demo`

Two scripted, self-running-on-scroll animations. Pure CSS/JS, no video, no external assets. Each ≤ 40 lines of JS. Purpose: teach the two concepts that moved most, in the medium they actually live in.

**Demo A — "What the sandbox actually blocks"** (Q5, +39.0 pp, the study's largest gain)

A faux terminal (dark kale panel, monospace, colored prompt) types out an agent attempting to fetch external API docs mid-task. The local file write succeeds in emerald. The outbound request hangs, then fails — sienna: `network unreachable (sandbox: workspace-write)`. Caption below: the default sandbox permits writes inside the working directory and blocks outbound network access. Half the cohort did not know this going in.

**Demo B — "Why a 600-line AGENTS.md stops working"** (Q3, +31.7 pp)

A two-pane before/after. Left: a scrolling file that grows from 80 to 600 lines, with commands and rules progressively drowning in a rising tide of rationale and history (dim the non-actionable lines as they accumulate). Right: the same content split — a lean AGENTS.md holding commands, paths, rules, and pitfalls, with history moved to separate task-specific files. Caption: rationale and history dilute signal.

**Requirements for both:** play once on scroll into view (IntersectionObserver, `threshold:0.4`), a `Replay` button, and under `prefers-reduced-motion` render the completed end state immediately with no typing animation. Never autoplay audio (there is none) and never trap scroll.

---

## 9. Accessibility and responsive

- **Contrast:** all text ≥ 4.5:1. Verify `--body #424D53` on `--almost-white` (passes) and every color used on `--darker-kale`. `--flat #9DBAB3` is decorative only — never text.
- **Never color-alone:** improved/declined must also differ by shape or label. Dot matrix gets a legend with distinct shapes or explicit hover text; dumbbell deltas carry signed numerals.
- **Keyboard:** the entire assessment, every toggle, every sort control, and every expandable row reachable and operable. Visible focus ring — 2px `--emerald` with 2px offset.
- **Semantics:** one `h1`. Sections in document order. Charts get `role="img"` with a meaningful `aria-label` summarizing the takeaway, plus a visually-hidden data table for the dumbbell and slopes so screen-reader users get the actual numbers.
- **`prefers-reduced-motion: reduce`:** disable `.fade` reveals, chart entry animation, FLIP reordering, and demo typing. Never gate content behind motion.
- **Breakpoints:** 1180 (max width) · 900 (findgrid collapse) · 820 (nav hides, stat strip wraps) · 640 (single column, quiz options full width, charts scroll). Test at 375px.
- Body must never scroll horizontally. Wide charts scroll inside their own `overflow-x:auto` container.

---

## 10. Build phases

Work in order. Each phase ends in an openable, working file.

**Phase 1 — Shell and design system.** Extract tokens, component CSS, and the base64 logo from the reference page. Build masthead, hero, stat strip, footer, and all 13 empty sections with headings and eyebrows. Wire `.fade` scroll reveal and the nav anchors. *Checkpoint: the page looks like a member of the research series before a single number is on it.*

**Phase 2 — Data layer.** Build `ITEMS` from `Pre_Post Survey Questions.md` and Appendices A/B; `SUMMARY`, `BASELINE`, `MODULES` from the paper. Ingest and anonymize participant data. Run the §5.4 reconciliation script and report results. *Checkpoint: every assertion passes, or the discrepancy is on Cory's desk.*

**Phase 3 — Prose.** Write sections 4, 5, 9, 10, 12, 13 in full. Apply the §4.5 tone rule ruthlessly. This is the phase most likely to be rushed; don't. The prose is what makes it readable, and the interactives are worth nothing if the argument between them doesn't hold. *Checkpoint: readable end to end with charts still absent.*

**Phase 4 — The assessment engine.** §7.2 in full, including results, distribution plot, timing, persistence, and share line. Largest single chunk of work. *Checkpoint: completable by keyboard alone, on a 375px viewport, and after a hard reload.*

**Phase 5 — Charts.** Dumbbell, dot matrix, slopes, module bars. Then wire the quiz→dumbbell overlay. *Checkpoint: every chart's numbers match §5 exactly; overlay appears only after a completed quiz.*

**Phase 6 — Guess widget and micro-demos.** §7.1 and §8.

**Phase 7 — Polish and QA.** Print styles, reduced-motion pass, contrast audit, the §11 checklist. Then read the whole page aloud once — it catches tonal problems nothing else does.

---

## 11. Verification checklist

Run every item. Report results explicitly; do not mark the build complete on assumption.

**Data integrity**
- [ ] All §5.4 assertions pass
- [ ] Every statistic rendered on the page traces to `SUMMARY` / `ITEMS` / `BASELINE` / `MODULES` — no literals hardcoded in markup
- [ ] Appendix A percentages and Appendix B transition counts match the paper exactly
- [ ] All 12 stems, 48 options, 12 correct answers, and 12 principle lines match `Pre_Post Survey Questions.md` verbatim
- [ ] Correct-answer key matches the §5.2 table (D,D,B,A,C,B,A,D,D,C,A,B)

**Privacy**
- [ ] `grep -iE "@|gmail|email|name" index.html` returns nothing but intentional copy — zero participant identifiers
- [ ] Participants referenced only as `p01`–`p41` or as anonymous dots
- [ ] No free-text participant responses anywhere in the file

**Standalone**
- [ ] Zero external requests: no `<link href="http`, no `<script src="http`, no remote `url(` in CSS
- [ ] Opens from `file://` with an empty console
- [ ] Renders correctly with the network disconnected

**Function**
- [ ] Assessment completable in both `full` and `quick` modes
- [ ] Fully keyboard-operable start to finish
- [ ] `localStorage` failure (simulate by throwing on `setItem`) does not break the page
- [ ] Quiz→dumbbell overlay appears after completion and only then
- [ ] Every sort control and toggle works and is keyboard-reachable
- [ ] Both micro-demos play on scroll and replay on demand

**Presentation**
- [ ] No horizontal body scroll at 375 / 768 / 1440
- [ ] `prefers-reduced-motion` honored across all six animated components
- [ ] Text contrast ≥ 4.5:1 throughout; no meaning conveyed by color alone
- [ ] Print output is legible with interactives suppressed
- [ ] §9's framing is exact: Q6/Q10/Q12 are "hardest after training"; Q9/Q10/Q12 "declined"; Q9's decline is labeled ceiling noise

**Editorial**
- [ ] Tone rule holds — no statistic sits inside a primary sentence
- [ ] Finding 02 cannot be misread as "training doesn't help senior engineers"
- [ ] The no-control-group limitation appears in section 12 *and* is acknowledged near the headline number
- [ ] Cohort geography stated factually in section 10, nowhere framed as novelty

---

## 12. Out of scope

- Embedded video of live sessions (deliberately replaced by §8 micro-demos)
- Server-side score collection or aggregation of reader results — everything stays client-side
- Multi-page site, routing, or a build pipeline
- Capstone and hackathon outcomes (explicitly not analyzed in the paper — do not speculate)
- Base64-inlined webfonts (noted as a possible follow-up in §4.2)
- Any comparison to other training programs or vendors
