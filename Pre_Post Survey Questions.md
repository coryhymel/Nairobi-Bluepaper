# **Quiz 4 — Final Assessment**

**Coverage:** Full curriculum — prompt structure, AGENTS.md, configurations, MCPs, skills, automations, multi-agent patterns, long-horizon execution, harness engineering, and the Codex SDK.

**Format:** 12 questions, multiple choice

**Estimated time:** \~10 minutes

---

1. **A developer has carefully reworded the same prompt four times. Each time the agent produces output that's on-prompt but doesn't fit the codebase's existing patterns. According to the power-user mindset, what is the most likely root cause and the right next step?**

* A) The model version being used lacks strong instruction-following — try a higher reasoning level  
* B) Prompt phrasing is still the bottleneck — more iterations will eventually yield the right result  
* C) The task is too complex — break it into three smaller prompts and run them sequentially  
* D) Context is the bottleneck — pass the agent existing files that demonstrate the patterns to match, via @ mention **✓**

*Principle: Instead of a perfect prompt, build perfect context. When agent output doesn't fit the codebase, the bottleneck is missing examples, not prompt phrasing.*

---

2. **A developer's prompts consistently produce output the agent marks as complete, but the result fails code review or breaks downstream tests. Which part of the prompt structure is most likely missing?**

* A) Goal — the agent doesn't know what outcome is desired  
* B) Context Pointers — the agent doesn't have enough relevant files to work from  
* C) Constraints — the agent isn't aware of style or convention rules it should follow  
* D) Done When — the agent has no clear verification criteria **✓**

*Principle: "Done When" specifies tests, checks, and expected behavior — without it, the agent has no objective signal of completion and will declare done at the first plausible stopping point.*

---

3. **A team's AGENTS.md started at 80 lines and has grown to 600 lines over six months — a mix of project conventions, architecture decisions, accumulating rationale, historical decisions, and explanations of past tradeoffs. Recently the agent's edits have started ignoring conventions that are clearly documented in the file. What is the most likely fix?**

* A) Split conventions, architecture, decisions, and rationale into separate files referenced from within AGENTS.md  
* B) Move historical and rationale content into separate task-specific .md files, and keep AGENTS.md focused on commands, paths, rules, and pitfalls **✓**  
* C) Convert the detailed sections into a series of skills so the agent only loads them when explicitly invoked  
* D) Add a structured table of contents so the agent can navigate to relevant sections efficiently

*Principle: AGENTS.md should be brief and actionable — commands, paths, rules, and pitfalls. Rationale and history dilute signal and degrade agent performance.*

---

4. **A team wants to: (1) have Codex automatically pull context from their Linear tickets, (2) package their "from issue to merged PR" workflow so any engineer can invoke it in one command, and (3) run a nightly dependency-drift scan without manual triggering. Which combination of team defaults covers all three?**

* A) An MCP for Linear context, a skill for the PR workflow, and an automation for the nightly scan **✓**  
* B) MCPs for both Linear and GitHub, plus an automation for the nightly scan  
* C) A single config.toml that references all three resources under \[mcp\_servers\]  
* D) A skill that chains all three steps with an automation to trigger the chain nightly

*Principle: Each team-defaults layer serves a distinct role — MCPs connect external tools, skills package repeatable workflows, automations schedule recurring tasks.*

---

5. **A newly-onboarded developer is debugging an issue where their agent fails to retrieve documentation from an external API mid-task. What is the most likely cause?**

* A) The agent requires authentication credentials to access external APIs during a session  
* B) External API access requires adding the service as an MCP server rather than calling it directly  
* C) The default sandbox mode allows local file writes but blocks outbound network access **✓**  
* D) Outbound network calls require setting the approval policy to never — with on-request, Codex pauses before each network call and the request times out waiting for input

*Principle: The default sandbox (workspace-write) allows writes within the working directory but blocks network access — a common surprise for developers who expect agents to reach external APIs out of the box.*

---

6. **A team needs two parallel agents: one to map service dependencies across a 300-file codebase without writing, and one to review a recent feature for security risks with instructions to write tests before flagging issues. A developer argues both should be `default` — "role names are just labels." What's the case against?**

* A) `default` agents serialize within a session — without specialization, the two tasks run sequentially  
* B) Specialized roles bundle reusable configuration — description, developer instructions, reasoning, and sandboxing — that travels with the role instead of being re-specified per prompt **✓**  
* C) `default` inherits the session's `workspace-write` sandbox; only `explorer` enforces the read-only access the dependency map requires  
* D) Role names map to different underlying models — `explorer` uses a faster model tuned for code traversal

*Principle: Specialized agent roles encode reusable configuration — the case for them is capability fit and reusability, not parallelism, sandbox inheritance, or model routing.*

---

7. **A team lead notices engineers are spending most of their time writing code and using Codex only for autocomplete and Q\&A. According to the operating model shift that high-performing agent-first teams have made, what should engineers be doing instead?**

* A) Designing intent, encoding context, and verifying outcomes — while agents handle execution **✓**  
* B) Writing only the hardest 20% of the code and delegating routine tasks to Codex  
* C) Reviewing every line Codex produces before committing, to maintain quality standards  
* D) Running Codex in parallel with their own implementation and committing whichever result is better

*Principle: "Humans steer. Agents execute." Engineering time moves from typing code to designing environments, intent, and feedback loops.*

---

8. **A developer assigns Codex a complex, multi-day implementation task and starts the run. An hour in, the agent has written substantial code but drifted from the original spec — adding features not requested and skipping parts that were. What structural investment, made before starting the run, would most likely have prevented this?**

* A) Setting the approval policy to never so the agent doesn't pause mid-task and lose context  
* B) Breaking the task into smaller, reviewable chunks and re-prompting between each so the developer can correct drift before it compounds  
* C) Running the task in a worktree so any drift is isolated and can be cleanly reverted  
* D) Building a structured planning document — with goals, milestones, and validation checkpoints — that the agent can anchor to throughout execution **✓**

*Principle: Long-horizon tasks require a planning artifact (spec \+ milestones \+ validation steps) for the agent to anchor to. Model settings don't substitute for structure.*

---

9. **A team has Codex writing fixes for reported UI bugs. The agent consistently produces code changes that are logically sound but miss the actual visual problem — fixing the wrong element or making changes that look right in code but break the layout. What structural change would most directly improve accuracy?**

* A) Require engineers to write more detailed bug reports with explicit file and line-number references  
* B) Switch to a multimodal model that can process screenshots natively in the prompt  
* C) Attach a screenshot of the broken UI to each bug-fix prompt so the agent can see the current state  
* D) Give the agent tools to observe the running UI directly — DOM snapshots, navigation, and live screenshots — so it can detect and verify visual state without human intermediation **✓**

*Principle: "If the agent cannot see it, it cannot fix it." The fix is making the product legible to the agent via live observability tools, not richer descriptions or one-time screenshot attachments.*

---

10. **A team is shipping a daily release and wants Codex to run a security review on every PR before it merges. The review needs to run in CI, post comments back to the PR, and gate the merge if it finds critical issues. Engineers should not have to manually invoke Codex for each PR. What's the right way to integrate Codex into this workflow?**

* A) Configure an automation in the Codex App scheduled to run hourly, scanning open PRs and posting comments via the GitHub MCP  
* B) Build a `pr-security-review` skill and have the GitHub Actions workflow run it via `codex exec $pr-security-review` on every PR event  
* C) Use the Codex SDK to call Codex from the CI pipeline on every PR event, with a structured output schema for findings that the CI job uses to gate the merge **✓**  
* D) Add the GitHub MCP to the team's config.toml and instruct AGENTS.md to run a security review whenever a PR is opened — Codex will pick up the instruction during normal sessions

*Principle: The Codex SDK is the right primitive for embedding Codex into existing pipelines (CI, scripts, internal tools) with structured outputs and event-driven control. Automations run on a schedule, not on events; skills package workflows but aren't designed as the integration surface for CI gating; AGENTS.md instructions only fire during interactive sessions.*

---

11. **A team has shifted to an agent-first workflow where four engineers each kick off two or three Codex tasks in parallel against the same repo — refactors, test additions, dependency upgrades, bug fixes. They quickly hit a problem: agents are stepping on each other's edits, and engineers are spending more time resolving merge conflicts between agent-generated changes than they're saving. What structural change addresses this most directly?**

* A) Have each agent run on its own worktree so changes are isolated to a separate branch per task, then review and merge through the normal PR flow **✓**  
* B) Add a shared lock file the agents check before editing, so only one agent can write to the repo at a time — sequencing the work eliminates the conflicts at the cost of some throughput  
* C) Have each engineer clone the repo into a separate directory per task and run agents against their own clone, merging back to the main repo manually at the end of the day  
* D) Configure each agent with a tighter \[sandbox\_workspace\_write\] scoped to a different subdirectory of the repo, so agents can only edit their assigned area

*Principle: Worktrees are the structural enabler for parallel agent work — isolated branches per task, normal PR review at the end. The other options either serialize the work, duplicate the repo, or artificially partition the codebase in ways that don't match real refactor scope.*

---

12. **A team's standard for handling on-call incidents lives in a Google Doc that gets updated after every postmortem. They've noticed Codex consistently proposes incident-response steps that contradict the current standard — pulling outdated patterns from somewhere, ignoring the team's actual playbook. The doc is the source of truth for humans, but Codex never reads it. What's the right fix?**

* A) Build an MCP server that connects to Google Docs so Codex can pull the current playbook into context whenever it's working on incident-related tasks  
* B) Encode the playbook as a markdown file checked into the repo (e.g., `docs/incident-response.md`) and reference it from AGENTS.md so it loads with every run **✓**  
* C) Have an engineer paste the current playbook into the prompt at the start of any incident-response task — it's a small one-time cost per incident, and it guarantees the latest version  
* D) Enable memories so Codex consolidates incident-response decisions from past sessions; over time the memory workspace will accumulate the team's standard

*Principle: "What Codex can't see doesn't exist." Durable team knowledge that lives outside the repo is invisible to the agent. The fix is to encode it as versioned markdown in the repo, not to build a connector to where it currently lives or to rely on memory of past sessions.*

