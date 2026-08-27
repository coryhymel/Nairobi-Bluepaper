# Measuring Knowledge Gains from Structured Training in AI-Assisted Software Engineering 

**Author:** C.Hymel  
**Version**: 1.0

## Abstract

AI coding systems increasingly operate as agents that can inspect repositories, edit files, run commands, call tools, and validate their own work. Effective use therefore requires developers to learn practices that extend beyond code completion, including context design, execution control, mechanism selection, and verification. This retrospective program evaluation examined whether a short, structured Codex learning program was associated with measurable changes in this applied knowledge among professional developers. The two-week online program combined asynchronous materials, four live sessions, guided practice, and two required module quizzes. Participants were mid- to senior-level engineers based in Africa with limited or no prior Codex exposure and used the Codex extension for Visual Studio Code. An identical 12-item scenario-based assessment was administered before and immediately after instruction. The paired analysis included 41 participants who completed both assessments. Mean performance increased from 69.1% to 80.7%, a gain of 11.6 percentage points (95% CI \[6.4, 16.8\], *p* \< .001, Cohen's *d*z \= 0.70). Twenty-four participants improved, 12 recorded the same score, and five declined by one item. The largest gains involved sandbox and network constraints, repository-context hygiene, verification criteria, parallel worktrees, and team-level configuration choices. These findings provide exploratory evidence that short, structured instruction can be associated with meaningful gains in assessed Codex workflow knowledge. 

**Keywords:** AI-assisted software engineering; coding agents; human–AI interaction; developer education; professional learning; Codex; pre–post evaluation

## 

## 1\. Introduction

Large language model–based programming tools have developed rapidly from source-code generation systems (Chen et al., 2021\) into agents capable of reading repositories, modifying files, running commands, calling external tools, and iterating against tests (Yang et al., 2024). This is fundamentally changing the developer's role. Effective use increasingly depends not only on writing or accepting code, but also on specifying intent, exposing relevant context, selecting appropriate mechanisms, constraining execution, and designing verification signals.

Research in human–computer interaction suggests that these practices are not acquired automatically through tool access. Programmers use AI assistants both to accelerate work they already understand and to explore unfamiliar solution spaces, with each mode requiring active evaluation of model output (Barke et al., 2023). Usability studies have found that code-generation systems can reduce effort while introducing new costs associated with understanding, debugging, and validating generated code (Vaithilingam et al., 2022; Mozannar et al., 2024). A survey of 410 developers likewise identified difficulty controlling AI programming assistants and obtaining output that satisfies functional and nonfunctional requirements as persistent barriers to use (Liang et al., 2024). In a security-focused experiment, participants with access to an AI assistant produced less secure code and were more likely to believe their code was secure, underscoring the need for verification and calibrated trust (Perry et al., 2023). These findings are consistent with broader human–AI interaction guidance emphasizing user control, correctability, and clear communication of system behavior (Amershi et al., 2019).

Evidence on outcomes is context-dependent. Peng et al. (2023) found that developers with access to GitHub Copilot completed a standardized programming task 55.8% faster than a control group. In contrast, a later randomized field study found that 16 experienced open-source developers took 19% longer across 246 tasks in mature repositories when early-2025 AI tools were permitted (Becker et al., 2025). A meta-analysis of 23 studies reported a moderate average productivity benefit with substantial heterogeneity, but no statistically significant aggregate effect on programming-learning outcomes (Maier et al., 2026). Educational research has also examined how code generators affect novice learning and task performance (Kazemitabaar et al., 2023). Together, these findings distinguish tool access, task performance, and learning as related but non-equivalent outcomes. **Less attention has been given to a different organizational question: whether experienced developers can acquire the operational knowledge needed to work with coding agents through a short professional learning intervention.**

This paper evaluates a two-week Codex learning program designed for mid- to senior-level engineers. The program used agent-first engineering as an instructional frame: engineers design intent, context, execution conditions, and feedback loops while delegating suitable execution work to an agent. The evaluation measures whether participants could recognize and select these practices in scenario-based questions.  
The research question and statistical framing were developed after data collection. The study is therefore exploratory and its estimates should be read as program-evaluation evidence rather than confirmatory evidence of causation.

## 2\. Method

### 2.1 Program and participants

The program was delivered online to professional developers based in Africa. Participants ranged from mid- to senior-level engineers and had limited or no prior experience with Codex. Some were affiliated with Andela through its talent network, while others had no prior Andela affiliation. All participants used the Codex extension for Visual Studio Code.

Instruction lasted two weeks and combined static materials for asynchronous study with four one-hour live sessions. Two live sessions supported each of two modules. The sessions followed a concept–demonstration–practice–support format and included real-time demonstrations, guided exercises, questions, and troubleshooting. The first module covered Codex foundations: setup, the agent loop, prompt and context design, planning, verification criteria, repository guidance, and common software-development workflows. The second addressed advanced workflows: configuration, permissions and sandboxing, reusable skills, Model Context Protocol connections, automations, memory, parallel work, code review, and longer-horizon execution. Each module ended with a 10-item quiz that participants were required to pass; retries were allowed.

After instruction, participants could begin a separate one-week capstone. No new learning activities were delivered during that period, and participants completed the post-program assessment before receiving access to the capstone. Capstone and subsequent hackathon outcomes are not analyzed in this paper.

The pre-program assessment recorded 82 attempts, of which 76 were completed. The post-program assessment recorded 47 attempts, of which 41 were completed. The paired sample consisted of the 41 participants who completed both assessments, matched using normalized email addresses. 

### 2.2 Measures and analysis

The primary instrument was an identical 12-item multiple-choice assessment administered before the program and immediately after the instructional phase. Items presented realistic scenarios covering context architecture, verification, repository guidance, execution constraints, mechanism selection, specialized roles, planning, UI observability, CI integration, parallel work, and source-of-truth strategy. The instrument was developed by Andela's internal Assessment Team and reviewed by subject-matter experts. It was created for the curriculum and was not an independently validated research scale.

Each response was scored as correct or incorrect. Total scores ranged from 0 to 12 and were converted to percentages. The principal outcome was the within-participant change in total score. A paired *t*\-test assessed mean pre–post change, and a Wilcoxon signed-rank test provided a distribution-free robustness check. The analysis also reported a 95% confidence interval and Cohen's *d*z, which standardizes the mean change by the standard deviation of participant-level change scores.

Secondary analyses described the number of participants who improved, remained stable, or declined; movement across score thresholds; completion time; item-level correct-response rates; and response transitions. Participants were also grouped post hoc by pre-program score: lower baseline (6 or fewer correct), middle baseline (7–8 correct), and higher baseline (9 or more correct). These groups are descriptive and were not prespecified.

## 3\. Results

### 3.1 Overall pre–post outcomes

Among the 41 matched participants, mean performance increased from 8.29 to 9.68 correct responses out of 12, equivalent to a change from 69.1% to 80.7%. The mean gain was **11.6 percentage points** (95% CI \[6.4, 16.8\]). The paired *t*\-test was statistically significant (*p* \< .001 ), and the Wilcoxon signed-rank test also returned *p* \< .0001. Cohen's *d*z was 0.70, indicating a moderate-to-large standardized within-participant change.

**Table 1\. Pre–post performance among matched participants (*n* \= 41\)**

| Metric | Pre-program | Post-program | Change |
| :---- | ----: | ----: | ----: |
| Mean correct responses | 8.29 / 12 | 9.68 / 12 | \+1.39 |
| Mean score | 69.1% | 80.7% | \+11.6 pp |
| Median correct responses | 8 | 10 | \+2 |
| Minimum correct responses | 4 | 6 | \+2 |
| Maximum correct responses | 12 | 12 | 0 |
| Median completion time | 18.5 min | 8.7 min | −9.8 min |

Twenty-four participants (58.5%) improved, 12 (29.3%) received the same score, and five (12.2%) declined by one item. No participant declined by more than one item, and 16 gained at least two additional correct responses. The share scoring at least 9 of 12 increased from 46.3% to 78.0%, while the number scoring 7 or fewer fell from 15 to four. 

Participants with lower starting scores recorded the largest gains. Those beginning with 6 or fewer correct responses improved by 3.45 items on average, compared with gains of 1.64 items for those beginning with 7–8 correct and 0.05 items for those beginning with 9 or more correct (Table 2).

**Table 2\. Score change by pre-program performance**

| Starting-score group | *n* | Mean pre | Mean post | Mean gain |
| :---- | ----: | ----: | ----: | ----: |
| Lower baseline (≤6/12) | 11 | 5.36 | 8.82 | \+3.45 |
| Middle baseline (7–8/12) | 11 | 7.64 | 9.27 | \+1.64 |
| Higher baseline (≥9/12) | 19 | 10.37 | 10.42 | \+0.05 |

Median completion time decreased from 18.5 to 8.7 minutes, and 36 participants (87.8%) completed the post-program assessment faster. Because participants answered the same questions twice, this change cannot be separated from test familiarity and is treated as secondary evidence rather than an independent measure of fluency.

### 3.2 Item and module patterns

The largest item-level gains occurred in practical operating mechanics. Correct responses increased by 39.0 percentage points for sandbox and outbound-network constraints, 31.7 points for repository-guidance hygiene, 26.8 points for verification criteria, 17.1 points for parallel worktrees, and 14.6 points for team-level configuration choices. Items covering the agent-first operating model, context as a bottleneck, and UI observation tools were already above 90% before the program or approached universal correctness afterward.

The most persistent difficulty involved selecting among adjacent implementation mechanisms. Post-program correctness was 70.7% for specialized roles, 41.5% for CI security-review integration, and 36.6% for durable source-of-truth context strategy. The full item table and participant-level response transitions are provided in Appendices A and B.

Both in-program modules reached a final pass rate of 100% because participants could retry. First-attempt and retry measures nevertheless indicated that the advanced module was more difficult (Table 3). Its average score was five percentage points lower, first-attempt pass rate was 14 points lower, and additional attempts per learner were 2.15 times higher. Item difficulty was also less uniform. Three questions accounted for 50.6% of Module 1 errors, while four accounted for 66.2% of Module 2 errors, suggesting that difficulty was concentrated in a relatively small set of concepts.

**Table 3\. Aggregate module performance**

| Metric | Module 1: Foundations | Module 2: Advanced Workflows |
| :---- | ----: | ----: |
| Quiz items | 10 | 10 |
| Distinct learners | 58 | 54 |
| Total attempts | 69 | 76 |
| Final pass rate | 100% | 100% |
| Average score | 87% | 82% |
| Aggregate item-correct rate | 87.4% | 82.1% |
| Average attempts per learner | 1.2 | 1.4 |
| First-attempt pass rate | 86% | 72% |
| Additional attempts | 11 | 22 |
| Additional attempts per learner | 0.19 | 0.41 |
| Standard deviation of item difficulty | 7.1 pp | 11.0 pp |

## 4\. Discussion

The central result is a statistically significant and practically meaningful increase in assessed Codex workflow knowledge following a two-week professional learning program. The average participant answered approximately 1.4 more of 12 scenario-based questions correctly, the confidence interval excluded trivial change, and a nonparametric test corroborated the paired *t*\-test. The distributional shift was also broad: nearly three-fifths of matched participants improved, fewer participants remained at the lower end of the score distribution, and declines were limited to one item.

We found that the pattern of gains is as important as the overall score change. The largest improvements concerned the environment around the agent: context hygiene, verification, execution constraints, isolated parallel work, and team configuration. Participants already performed well on the broad agent-first principle that humans should specify intent and verify outcomes while agents execute appropriate tasks but their remaining difficulty emerged when multiple agentic mechanisms appeared plausible. This distinction suggests that strategic understanding and operational judgment develop at different rates. 

The baseline-group results also offered an interesting insight. Participants entering with the lowest assessment scores improved most, while the highest group changed little. A plausible interpretation is that the program helped establish a more consistent foundation among learners with limited initial knowledge. However, the fixed 12-item scale offered less headroom to high scorers and may have been insufficiently difficult to detect advanced learning. The result should not be used to conclude that experienced or high-baseline participants received no benefit.

Several limitations constrain the strength and generalizability of the findings. Most importantly, the evaluation had no control group. The identical pre- and post-assessment may have increased both scores and speed through familiarity. However, participants received no scores or answer feedback after the pre-test, so familiarity could plausibly affect completion time and may have primed attention to certain topics during instruction, but it does not by itself explain correct responses on items previously answered incorrectly.

## 5\. Conclusion

Professional developers scored higher on a scenario-based Codex knowledge assessment after completing a two-week structured learning program. Among 41 matched participants, mean performance increased by 11.6 percentage points, with a moderate-to-large standardized change and convergent results across paired statistical tests. Gains were strongest in practical operating concepts, while advanced mechanism selection remained comparatively difficult.

The study should be interpreted as exploratory program-evaluation evidence rather than causal proof. Even with that constraint, it provides a useful signal for engineering and learning leaders: access to a coding agent and proficiency with that agent are not the same, and a short instructional intervention can be associated with measurable movement in the knowledge developers use to structure agentic work. Future research should determine whether these gains persist and translate into higher-quality, safer, or more productive engineering outcomes.

## 

## References

Amershi, S., Weld, D., Vorvoreanu, M., Fourney, A., Nushi, B., Collisson, P., Suh, J., Iqbal, S., Bennett, P. N., Inkpen, K., Teevan, J., Kikin-Gil, R., & Horvitz, E. (2019). Guidelines for human–AI interaction. *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems*, 1–13. [https://doi.org/10.1145/3290605.3300233](https://doi.org/10.1145/3290605.3300233)

Barke, S., James, M. B., & Polikarpova, N. (2023). Grounded Copilot: How programmers interact with code-generating models. *Proceedings of the ACM on Programming Languages, 7*(OOPSLA1), 85–111. [https://doi.org/10.1145/3586030](https://doi.org/10.1145/3586030)

Becker, J., Rush, N., Barnes, E., & Rein, D. (2025). Measuring the impact of early-2025 AI on experienced open-source developer productivity. *arXiv*. [https://doi.org/10.48550/arXiv.2507.09089](https://doi.org/10.48550/arXiv.2507.09089)

Chen, M., Tworek, J., Jun, H., Yuan, Q., Pinto, H. P. de O., Kaplan, J., Edwards, H., Burda, Y., Joseph, N., Brockman, G., Ray, A., Puri, R., Krueger, G., Petrov, M., Khlaaf, H., Sastry, G., Mishkin, P., Chan, B., Gray, S., ... Zaremba, W. (2021). Evaluating large language models trained on code. *arXiv*. [https://doi.org/10.48550/arXiv.2107.03374](https://doi.org/10.48550/arXiv.2107.03374)

Kazemitabaar, M., Chow, J., Ma, C. K. T., Ericson, B. J., Weintrop, D., & Grossman, T. (2023). Studying the effect of AI code generators on supporting novice learners in introductory programming. *Proceedings of the 2023 CHI Conference on Human Factors in Computing Systems*, Article 455, 1–23. [https://doi.org/10.1145/3544548.3580919](https://doi.org/10.1145/3544548.3580919)

Liang, J. T., Yang, C., & Myers, B. A. (2024). A large-scale survey on the usability of AI programming assistants: Successes and challenges. *Proceedings of the 46th IEEE/ACM International Conference on Software Engineering*. [https://doi.org/10.1145/3597503.3608128](https://doi.org/10.1145/3597503.3608128)

Maier, S., Gunzenhäuser, M., Schweisthal, J., Schneider, M., & Feuerriegel, S. (2026). A meta-analysis of the effect of generative AI on productivity and learning in programming. *arXiv*. [https://doi.org/10.48550/arXiv.2605.04779](https://doi.org/10.48550/arXiv.2605.04779)

Mozannar, H., Bansal, G., Fourney, A., & Horvitz, E. (2024). Reading between the lines: Modeling user behavior and costs in AI-assisted programming. *Proceedings of the 2024 CHI Conference on Human Factors in Computing Systems*, Article 100\. [https://doi.org/10.1145/3613904.3641936](https://doi.org/10.1145/3613904.3641936)

Peng, S., Kalliamvakou, E., Cihon, P., & Demirer, M. (2023). The impact of AI on developer productivity: Evidence from GitHub Copilot. *arXiv*. [https://doi.org/10.48550/arXiv.2302.06590](https://doi.org/10.48550/arXiv.2302.06590)

Perry, N., Srivastava, M., Kumar, D., & Boneh, D. (2023). Do users write more insecure code with AI assistants? *Proceedings of the 2023 ACM SIGSAC Conference on Computer and Communications Security*, 2785–2799. [https://doi.org/10.1145/3576915.3623157](https://doi.org/10.1145/3576915.3623157)

Vaithilingam, P., Zhang, T., & Glassman, E. L. (2022). Expectation vs. experience: Evaluating the usability of code generation tools powered by large language models. *CHI Conference on Human Factors in Computing Systems Extended Abstracts*. [https://doi.org/10.1145/3491101.3519665](https://doi.org/10.1145/3491101.3519665)

Yang, J., Jimenez, C. E., Wettig, A., Lieret, K., Yao, S., Narasimhan, K., & Press, O. (2024). SWE-agent: Agent-computer interfaces enable automated software engineering. *Advances in Neural Information Processing Systems, 37*. [https://doi.org/10.52202/079017-1601](https://doi.org/10.52202/079017-1601)

## 

## Appendix A. Complete Pre–Post Item Results

| Item | Assessed concept | Pre correct | Post correct | Change |
| :---- | :---- | ----: | ----: | ----: |
| Q1 | Context as the bottleneck | 90.2% | 92.7% | \+2.4 pp |
| Q2 | Verification criteria | 61.0% | 87.8% | \+26.8 pp |
| Q3 | Repository-guidance hygiene | 58.5% | 90.2% | \+31.7 pp |
| Q4 | Team defaults | 73.2% | 87.8% | \+14.6 pp |
| Q5 | Sandbox and network constraints | 51.2% | 90.2% | \+39.0 pp |
| Q6 | Specialized agent roles | 58.5% | 70.7% | \+12.2 pp |
| Q7 | Agent-first operating model | 97.6% | 100.0% | \+2.4 pp |
| Q8 | Planning artifacts for long tasks | 80.5% | 90.2% | \+9.8 pp |
| Q9 | UI observation tools | 97.6% | 92.7% | −4.9 pp |
| Q10 | CI security-review integration | 46.3% | 41.5% | −4.9 pp |
| Q11 | Worktrees for parallel agent work | 70.7% | 87.8% | \+17.1 pp |
| Q12 | Durable source-of-truth context | 43.9% | 36.6% | −7.3 pp |

## Appendix B. Item Response Transitions

| Item | Wrong → Correct | Correct → Wrong | Stayed correct | Stayed wrong |
| :---- | ----: | ----: | ----: | ----: |
| Q1 | 4 | 3 | 34 | 0 |
| Q2 | 13 | 2 | 23 | 3 |
| Q3 | 13 | 0 | 24 | 4 |
| Q4 | 8 | 2 | 28 | 3 |
| Q5 | 18 | 2 | 19 | 2 |
| Q6 | 8 | 3 | 21 | 9 |
| Q7 | 1 | 0 | 40 | 0 |
| Q8 | 5 | 1 | 32 | 3 |
| Q9 | 0 | 2 | 38 | 1 |
| Q10 | 4 | 6 | 13 | 18 |
| Q11 | 8 | 1 | 28 | 4 |
| Q12 | 4 | 7 | 11 | 19 |

