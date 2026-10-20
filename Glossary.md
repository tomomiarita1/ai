# AI Evals: Course Glossary

*A cumulative reference for the terms used across all 6 modules. Use it as a quick lookup when something on a slide or in your repo work doesn't quite click.*


The glossary has 6 sections, one per module:

1. **Module 1: Foundations of AI Evaluation**
2. **Module 2: Failure Taxonomy and Root Cause**
3. **Module 3: Building Eval Suites**
4. **Module 4: CI Gates and Deployment**
5. **Module 5: Coverage, Budget and Trade-offs**
6. **Module 6: Capstone, Ship Your Eval Stack**

---

## Module 1: Define What Good Looks Like for an AI Feature

> Module-specific terminology introduced in Module 1: Define What Good Looks Like for an AI Feature.
> Cross-module glossary lives at [Glossary.md](Glossary.md) (forthcoming, populated as the cert ships).

---

### Accuracy (Lab Metric)
The percentage of model outputs that match a predefined "correct" answer on a static test dataset. Excellent in a controlled lab, **blind to UX, trust, safety, and latency in production**. The 95% Accuracy Trap is what happens when you confuse this with product quality.

### AI Evaluation Strategy Canvas
The 3-section worksheet (Product Strategy → Measurements → Strategic Trade-Offs) that captures *what "good" means* for an AI product before any code or evaluator is written. Lives at [`Module 1 - Lab Guide.html#activity-2`](Module%201%20-%20Lab%20Guide.html#activity-2). The output becomes the Strategy Canvas slide of the Final Project Deliverables deck.

### Bias
See **Fairness**. When a model's output quality is uneven across user groups, demographics, geographies, personas, languages, it has bias. Bias creates both reputational and **regulatory** risk and limits Total Addressable Market.

### Code-Based Evals
Automated pass/fail checks run by pre-written code against AI output. Fastest, cheapest, and infinitely scalable. Strong for functional correctness (Gmail spam classification, GitHub Copilot unit tests, Notion data extraction). **Blind to nuance, tone, and reasoning quality.**

### Conciseness Evaluator
The specific LLM-as-a-Judge evaluator used in the Module 1 eval lab. Scores a model's output on how concise it is on a 1 to 5 scale. Used to demonstrate that prompt design (Version A: ultra-concise vs Version B: narrative) is a measurable lever.

### Deterministic System
A system where the same input always produces the same output. The classic software-engineering target. Banking ledgers, payments, exact-match search. **Does not need evals**: standard QA suffices.

### Drift (Model Drift)
A slow degradation in model performance over time, typically because the underlying data distribution shifts (new user behavior, new content, new edge cases). Background Monitoring exists to catch drift before it becomes a crisis.

### Eval (Evaluation)
A systematic test of an AI's behavior, designed to measure if the system meets a product-specific definition of "good" across dimensions like accuracy, trust, safety, and latency. Unlike traditional ML benchmarks, evals are **contextual**: they measure how well a system works in *your product, for your users, under real-world conditions*.

### Eval-as-PRD
The 2026 operating frame that an eval is the *modern version of a Product Requirements Document*, an **executable** definition of "good" that both states a requirement and checks it on every change, rather than describing it in prose. Coined by Ankur Goyal (Braintrust, Lenny's Newsletter, Jun 2026). Its companion idea: shipping trustworthy AI is "a trust problem, not a tooling problem" (Elena Verna, Jun 2026), evals are that trust infrastructure, not a platform you can buy.

### Eval Gates
Automated thresholds wired into the CD/CC (continuous deployment / continuous calibration) pipeline. Block a release if Hallucination Rate > 5%, Latency > 1s, etc. Covered in detail in Module 4.

### Eval Spec
The structured document that defines *what* an evaluator measures, *how* it measures it, and *what threshold* counts as pass. Drafted in Module 3.

### Fairness
The degree to which a model's output quality is consistent across different user groups (demographics, personas, languages, geographies). A high fairness score means the model performs equally well for every segment of your audience.

### Failure Taxonomy
A formal categorisation of the unique failure modes of your AI product. Built in Module 2. Each failure mode gets prioritised P0 to P3 by business impact.

### False Negative
The model lets a harmful or undesirable output **slip through** when it should have been blocked. Liability risk. Example: an unsafe legal response that should have been guardrailed.

### False Positive
The model blocks (or refuses to handle) a **legitimate** output. Engagement / UX-trust risk. Example: a content classifier flagging a normal customer-service message as unsafe.

### Flywheel Effect (Eval Trust Loop)
The compounding cycle in which evals → reveal failure patterns → drive improvements → enable better evals → and so on. The engine of confident, high-velocity AI product iteration.

### Golden Dataset / Golden Set
A high-quality, human-rated set of AI outputs that serves as the ground truth for validating automated evaluators. The Human Eval cost is justified primarily by producing this golden set, which then anchors cheaper LLM-as-a-Judge evaluators.

### Guardrails
Active interventions that sit in the **critical path** of an AI response, blocking, retrying, or routing to a safer fallback before the user sees the output. The most direct PM lever for managing real-time compliance and ethical risk.

### Hallucination
A confident, plausible-sounding output that is factually false or fabricated. The single most viral failure mode in AI products. Measured by **Hallucination Rate**: % of outputs containing false information against standard input.

### Human Evals
Qualified human experts scoring AI outputs against a detailed quality rubric. Highest fidelity available, captures trust, tone, ethical and legal nuance. Slow, expensive, hard to scale. The mechanism for establishing the golden set.

### LangSmith
A LangChain-developed observability and evaluation dashboard for LLM applications. In this course it's an **optional** dashboard (alongside Braintrust or Phoenix) for capturing traces and monitoring production; the labs themselves run in any AI chat, so no LangSmith account is required.

### Latency
The time elapsed between a user sending a request and the model returning a complete response. **Measure at P95 or P99, never average.** P95 forces your team to fix the frustrated tail.

### LLM-as-a-Judge
An evaluation method where a powerful "judge" LLM automatically scores another model's outputs against a quality rubric. Scales human-style semantic judgement at a fraction of the cost. Must be validated against the human golden set to be trusted.

### Probabilistic AI System
A system where the same input can produce a *range* of different, variable outputs, by design. ChatGPT, Claude, Gemini and every modern LLM are probabilistic. Quality control here means defining and measuring acceptable variability, not pass/fail unit tests.

### Robustness
The percentage of responses that remain coherent and accurate when faced with messy, adversarial, or out-of-scope input. Tests how the AI handles the chaos of the real world.

### Strategic Trade-Off
A pre-decided sacrifice of one metric to win on another. Documented as: *"We prioritize [X] over [Y] because [strategic reason grounded in user and business context]."* The Strategy Canvas forces every team to commit two of these before code is written.

### Trajectory Evaluation
Scoring the **path** an AI takes to an answer, not just the answer itself, the tools it called, the order and arguments of those calls, whether it looped or retried needlessly, and how it recovered after a failed step. Distinct from **output evaluation** (judging only the final response). For agentic products like Ascend IQ, final-answer pass/fail is now table stakes; trajectory evaluation is the 2026 frontier. Introduced in Module 1, taught as a first-class skill in Module 3.

### Triangulation
The PM practice of comparing direct evaluation results (Code · Human · LLM-as-a-Judge) with User & Business metrics to isolate whether a problem is a real output-quality issue or a user-expectation issue.

### Trust Gap
The new blind spot AI introduces between *what users do* (clicks, sessions, completions) and *whether the output was actually trustworthy, accurate, fair, or safe*. Old analytics tools (Amplitude, Mixpanel) cannot close it.

### User & Business Metrics
Real-world adoption signals, thumbs up/down, retention, task completion rate, NPS. The ultimate reality check. **Noisy**: never use without triangulating against direct evals.

### UX Trust
The user's subjective rating of the AI's predictability, clarity, and consistency over time. Closely tied to long-term retention and feature stickiness.

### Vibe Check
The pre-eval era anti-pattern of testing AI subjectively, "this prompt feels better than that one." Replaced by evals as soon as iteration cycles compound. Banned from the Development phase of any AI product.

---

## Module 2: Build a Failure Taxonomy by Business Impact

> Module-specific glossary for Module 2: Build a Failure Taxonomy by Business Impact.
> Cross-cutting AI Evals terms live in the [main Glossary](Glossary.md).

---

### Agentic failure modes
Failure types specific to AI **agents**: systems that plan, call tools, and act in steps, rather than single-shot chatbots. They hide in the agent's *trajectory*, not its final answer, so a response can read perfectly while the path that produced it was broken. The four to tag in Module 2: **Tool misuse**, **Reasoning loop**, **Permission / scope escalation**, and **Recovery failure**. Captured by reading the trace, then added as rows in the Failure Taxonomy alongside the Trust Metric tags.

### Business Impact Statement
A one-sentence translation of a technical failure into executive language. Format: *"This failure matters because [Technical Error] results in [Business Consequence]."* Lives in the Failure Taxonomy Canvas next to the #1 ranked risk.

### Bottom-up eval
A failure found by comparing model output to human edits or production traces, not written from the spec in advance. Models are weak at inventing these. Confirm on 10 to 20 examples before promoting the miss to an eval row. Pair with **Top-down eval**.

### Capture · Label · Cluster · Map
The four-step error-analysis framework introduced in Module 2. **Capture** raw outputs (good + bad) → **Label** with Trust Metrics → **Cluster** into systemic patterns → **Map** into a formal Failure Taxonomy. Cluster + Map are how a confirmed bottom-up finding becomes a taxonomy row.

### Criteria drift
The phenomenon where you discover what "good" means by labeling traces, not by writing the rubric first. Automated error-analysis tools miss this class of failure until a human names it.

### Cartographer Mindset
The PM disposition of documenting failures as a map. *"You can't manage what you haven't mapped."* The output is the Failure Taxonomy, your strategic terrain map that tells engineering exactly which evaluators to build first.

### Cost Curve (1× / 10× / 50× / 100×)
The multiplier on a failure's cost based on the lifecycle stage at which it is found. Discovery = 1× (cheap), Development = 10× (costly), Deployment = 50× (painful), Post-Launch = 100× (catastrophic). The Severity × Frequency matrix is your tool for catching P0s at 1×.

### Crisis Zone (P0)
The high-severity × high-frequency quadrant in the Risk Matrix. A failure here is a product-killer. Immediate hotfix; must be entirely gated.

### Doctor Mindset
The PM disposition of diagnosing root causes rather than treating symptoms. *"Why was the output bad?"*, was it a prompt issue, a RAG issue, or a model limitation? Required before any model-swap or prompt change.

### Failure Taxonomy
A formal table documenting every recurring failure pattern in an AI product. Each row contains: Failure Type · Trust Metric Tag · Observed Frequency · Severity · Business Impact. The **executive-facing risk artifact** of failure discovery.

### Failure Taxonomy Canvas
The structured template used to build a Failure Taxonomy in a single workshop session. M2 lab tool, exports markdown to `02-failure-discovery/failure-taxonomy.md`.

### Frequency (in the matrix)
The count of a specific Trust Metric tag across the dataset. **Threshold = 3** for the Ascend IQ audit (≥3 = High, ≤2 = Low). Always computed *per tag*, not per failure type.

### Gold Standard
The verified-correct examples in your dataset used to validate AI outputs. In most runners, this is the `reference` column of the Ascend IQ logs.

### Ground Truth
Synonym for Gold Standard. The objective answer the AI's response is compared against during evaluation.

### Guardrail (override case)
A justified refusal by the AI of an unsafe query. When the LLM-as-Judge flags a refusal as a failure, the PM overrides to PASS, the guardrail worked as intended. Returns again in Module 4 as a feature of eval gates.

### Hidden Risks (P1)
The high-severity × low-frequency quadrant. Rare but catastrophic. Demands proactive guardrails *before* the failure happens (lawsuits, brand exposure).

### LLM-as-a-Judge
A pattern where one LLM evaluates another LLM's outputs. The M2 lab configures a fast judge model, ideally from a *different model family* than the system under test, to avoid self-preference bias, as a "QA Analyst" judging the Ascend IQ agent's responses against the verified Ground Truth. The model is swappable; the rubric is what matters.

### Low Priority (P3)
The low-severity × low-frequency quadrant. Real bug, small segment, low impact. Backlog by default; only prioritize if it aligns with a larger strategic goal.

### Model Swap (trap)
The anti-pattern of reaching for a "better" or newer model without a root-cause diagnosis. A model swap is *rarely* the fix, it wastes budget and skips the diagnosis that would have surfaced the real underlying issue (data, prompt, retrieval, tool routing, or an eval gap). McDonald's drive-thru AI is the textbook case, the LLM wasn't the problem; the speech-to-text integration was. Change the model only once the evidence actually points at the model.

### Override
The human-PM act of correcting an LLM-as-Judge score during the audit. Most commonly: a `0 (FAIL)` judge score for a justified refusal gets overridden to `1 (PASS)`.

### P0 / P1 / P2 / P3
Severity levels in the Risk Matrix. P0 = Crisis Zone (block the launch). P1 = Hidden Risks (proactive guardrails). P2 = User Annoyances (acceptable debt). P3 = Low Priority (backlog).

### QA Analyst Prompt
The System Prompt used in the M2 lab to configure a fast judge model as a meticulous Quality Assurance evaluator. Defines the three failure criteria (Hallucination, Robustness, Fairness/Bias) and the strict JSON output format. The judge model is provider-neutral and swappable, pick one from a different model family than the system under test.

### Reasoning loop
An agentic failure mode: the agent repeats the same step without making progress and never terminates, re-running the same query, re-reading the same document, burning tokens until it times out. Spotted in the trajectory as repeated near-identical steps where the step count climbs but no new information arrives.

### Recovery failure
An agentic failure mode (also "bad recovery"): after a tool call fails (timeout, error, empty result), the agent doesn't recover gracefully, it gives up, fabricates a result to fill the gap, or retries blindly forever instead of degrading sensibly or asking for help. Found by inspecting the step *after* a failed tool result in the trajectory.

### Risk Matrix
The 2×2 Severity × Frequency grid that yields the P0 → P3 priorities. Tactical tool for sequencing fixes by business risk, not by engineering effort or frequency alone.

### Severity vs Frequency (the rule)
*Prioritize by severity, not by frequency.* A P0 that happened once outranks a P2 that happens 1,000× per day, because the cost of a P0 is catastrophic regardless of cadence.

### Strategic Framing
The PM communication discipline of connecting a technical fix to a business outcome (adoption · compliance · trust · retention). Distinguishes a Strategic PM from a Tactical PM.

### Symptom vs Root Cause
The diagnostic distinction. *"The bot is hallucinating"* is the symptom. *"Our RAG is pulling cached pricing data"* is the root cause. PMs are responsible for naming the root cause before proposing a fix.

### Top-down eval
A rule you write from the Module 1 definition of good, before you look at traces. Example: "every takeaway is 240 to 330 characters." Models are good at inventing these from a task description. Necessary, and not sufficient. Pair with **Bottom-up eval**.

### Tool misuse
An agentic failure mode: the agent calls the wrong tool for the job, or the right tool with the wrong arguments (e.g., Ascend IQ calls the `competitor_pricing` tool when the user asked about headcount, or queries the right tool with the wrong company ticker). Visible in the trajectory at the tool-call step, where the tool name and argument payload don't match the user's intent.

### Trajectory
The ordered sequence of an agent's reasoning steps, tool calls, tool arguments, tool results, and recovery attempts that produced an output. The *path*, not just the *destination*. For agents, you evaluate the trajectory, not only the final answer, because agentic failure modes (tool misuse, reasoning loops, scope escalation, recovery failure) are invisible to a final-answer audit. Captured from the run's trace in your eval/observability tool.

### Trust Metric Tag
The label attached to a confirmed failure during the Label step. The four tags used in Module 2: `#HALLUCINATION`, `#UX_TRUST`, `#ROBUSTNESS`, `#FAIRNESS`. Each maps to a category of judge-reasoning phrases.

### User Annoyances (P2)
The low-severity × high-frequency quadrant. Chronic UX degradation (robotic tone, latency lag). Acceptable technical debt; addressed in future optimization cycles.

### Vanity Metric (trap)
The anti-pattern of relying on a single high-level number (e.g., "95% accuracy") that hides rare-but-catastrophic failures. Air Canada's chatbot was highly accurate in aggregate; one fabricated bereavement-fare policy still cost the company a tribunal ruling.

### Vibe Check (banned)
The non-rigorous habit of declaring an AI output "fine" or "off" based on subjective feel. Not a scalable or defensible process. Module 2 is the explicit retirement of the vibe check in favor of structured error analysis.

---

## Module 3: Translate Failures Into Systematic Eval Suites

> Vocabulary for the cohort. Use this list when reviewing the [Module 3 deck](Module%203%20-%20Slides%20%28Shareable%29.html), the [Notes](Module%203%20-%20Notes%20%28Shareable%29.html) and the [Lab Guide](Module%203%20-%20Lab%20Guide.html).

---

## Evaluators

**Evaluator.** A test that catches one failure before a user does. If your Module 2 failure taxonomy tells you which failures matter most, an evaluator is what guards against one of them.

**Eval suite.** The set of evaluators you build for a product. Every P0 and P1 failure in your taxonomy needs at least one evaluator in it.

**Code-based check (the guardrail).** A deterministic rule, such as a phrase that must appear or a number that must match the source. Cheap, instant and the same every time. Use it for rules with no exceptions. _Stripe's refund gate is the example._

**LLM-as-judge (the scalable editor).** A model that grades another model's output against a rubric. Use it for things a rule can't see, such as tone or a misleading answer, at a volume people can't read. Use a judge from a different model family than the agent, because a model tends to rate its own family's writing higher. _Grammarly's tone warning is the example._

**Human review (the gold standard).** Experts review a sample of high-stakes outputs to provide ground truth from outside the model. The slowest and most expensive evaluator, so save it for the calls that matter most. _Intuit's CPA audit is the example._

**Golden dataset.** A set of answers your team has verified and treats as ground truth. Human reviewers keep it up to date.

**The eval suite pyramid.** How the three evaluators work together. Code-based checks run on everything and filter out obvious failures, the judge handles the cases that need judgment, and people review the small set where the stakes are highest.

---

## Writing a check

**The four questions.** Every check, whether it's a rule or a judge, answers the same four: what does it look at, what counts as a pass, what counts as a fail, and what does it return.

**Pass and fail conditions.** The specific, visible conditions a check uses to decide. A good fail condition is written so two people would make the same call with it.

**Rule check.** In Lab 1, a pass or fail rule a script could run, such as a phrase that must appear or a number that must match the reference.

**Safety rule.** In Lab 1, a rule that must hold every time, such as a kind of question the agent must always decline.

**Judge prompt.** In Lab 1, the check for what a rule can't see. It returns 1 or 0 plus one line of reasoning.

---

## Reading your results

**Real case.** A row your Module 2 audit confirmed as the failure you're testing for.

**Miss.** A real case the check passed. Misses are the dangerous ones, because you believe you're protected when you're not.

**False alarm.** A row your audit passed that the check failed. False alarms create noise and block answers that were fine.

**The Win.** The rule check or the safety rule caught the failure. A fast, cheap rule handles this risk, as long as it caught the real problem and not just a pattern on the surface.

**The Insight.** Only the judge caught the failure. The risk is about meaning, which a rule can't see, so the judge earns its cost.

**The Gap.** Nothing caught the failure. Your checks are too loose.

**P0 row.** The one row from the 20 Ascend IQ answers that shows your #1 failure. It carries through to your Final Project deck.

---

## Trajectory evaluation

**Trajectory.** The sequence of steps an agent takes to answer a question, such as which tools it called, with which arguments and in what order.

**Trajectory evaluation.** Scoring the path an agent took as well as its final answer. A path can break even when the final answer reads well.

**The six trajectory dimensions.** (1) **Tool selection:** did it call the right tool? (2) **Argument correctness:** were the arguments right? (3) **Redundant or looping:** did it repeat or loop? (4) **Recovery:** did it recover after a failed step? (5) **Plan coherence:** did the sequence make sense? (6) **Task completion:** did it finish the job?

**Reference path.** The steps an agent should take for a task. You score the actual path by comparing it with the reference, and count it as a match when it took the same steps in any order.

---

## Coverage

**Coverage matrix.** A table with one row per failure and one column per evaluator, showing which failures each evaluator covers and how strong that coverage is.

**Strong coverage (defense in depth).** Covered by a code-based gate, or by two probabilistic checks, such as an LLM judge plus human review. Required for every P0 and P1 failure.

**Medium coverage (single thread).** Covered by one probabilistic check, such as an LLM judge alone, or only by monitoring after launch. Acceptable for P2 and P3.

**Weak coverage (reactive only).** No test before launch. You find out when users complain. Acceptable for P3 only.

---

## The eval spec

**Eval spec.** The document that turns your top failure into a requirement engineering can build against. It lives in `03-eval-suites/eval-spec.md` in your repo.

**The five parts.**

1. **Target risk:** what are you testing? The failure, its trust metric, and whether it's an output or a trajectory risk.
2. **Evaluator:** how will you detect it? A code-based check, an LLM judge or human review. For a trajectory risk, name the dimensions you score.
3. **Threshold:** what is the pass/fail line? The exact number required to ship.
4. **Business stakes:** why does it matter? The cost of failure, such as churn, a lawsuit or damage to the brand.
5. **Owner:** who monitors and enforces it? The person accountable for the sign-off.

**Acceptance criteria.** The engineering message: the exact pass and fail rule, so nobody has to guess what to build. _Example: block any answer whose interest rate doesn't match the rates database exactly._

**Fallback.** The design message: what the user sees when a check blocks an answer, instead of an error or a blank screen.

**Risk and return.** The leadership message: the risk the spec removes, and why it's worth the cost.

---

## What's coming in Module 4

**Eval gate.** A pass/fail check tied to an eval spec's threshold, built into the release process so a change that breaks it can't ship.

**Threshold in a PRD.** Writing the eval spec's threshold into the product requirements document, so it becomes a launch criterion.

(Both terms get the full treatment in Module 4.)

---

## Module 4: Ship Safely with Eval Gates

> Vocabulary for the cohort. Use this list when reviewing the [Module 4 deck](Module%204%20-%20Slides%20%28Shareable%29.html), the [Notes](Module%204%20-%20Notes%20%28Shareable%29.html) and the [Lab Guide](Module%204%20-%20Lab%20Guide.html).

---

## The development loop

**Tuned trust loop.** The AI product lifecycle as two halves that meet at the eval gate: a precision cycle before launch and a trust cycle after it.

**Precision cycle.** Before launch: scope the AI capability, build the core feature and design the eval, so the product is healthy before it reaches a user.

**Trust cycle.** After launch: run evals on real traffic, group the failure patterns and ship improvements. This is how a product earns more autonomy over time.

---

## Gates

**Evaluator.** A test that measures one quality metric, such as hallucination rate. It reports a score and does nothing with it.

**Eval gate.** An automated checkpoint that compares an evaluator's score with a threshold and decides whether a release goes ahead.

**Advisory check.** A gate that warns and never blocks the release. Use it for low risks you want to track.

**Soft gate.** A gate that pauses the release until someone signs off on a documented override. Most gates should be Soft.

**Hard gate.** A gate that blocks the release until the issue is fixed, with no override. Save it for critical P0 risks.

**No gate.** The call for an answer the eval flagged by mistake, such as a refusal that followed the safety guidelines. Gating correct behavior blocks a safe product and creates alert fatigue.

**Kill switch.** A Hard gate at release, the last line of defense before customers see a change.

---

## Where gates run

**Pull request.** Where quick code-based checks run on every change, without calling the AI model. Most failures should be caught here.

**Staging.** Where the full eval suite runs with LLM-as-a-judge against the golden set, before release. Most Soft gates live here.

**Release.** The last check before customers see a change. Hard gates only.

---

## The golden set and CI

**Golden set.** A fixed set of cases you check every change against. Each case is an input and its verified correct output. A regression golden set holds the real cases the product must never get wrong again.

**Case types.** The four kinds of case that belong in a golden set: failures you've fixed, common requests, edge cases near a threshold, and must-refuse requests.

**Regression.** A drop in a check's score compared with the current version. A regression on a P0 or P1 case fails the gate.

**CI eval gate.** A gate that runs your checks automatically on every pull request and blocks the merge if one fails. Engineering adds it to the GitHub Actions workflow.

**Gate policy.** The PM's choices for a CI eval gate: which checks run, how far each can drop, and which ones block the merge and which only warn.

---

## The PRD

**Release criteria.** The PRD section that sets the quality a product needs before it can ship. For an AI product, this is where the eval gates live.

**Threshold.** The exact pass or fail number for a gate, such as "hallucination rate under 5%."

**Five parts of a threshold.** The metric, the gate level, the threshold value, the dataset and the evaluator.

**CI gate request.** The hand-off to engineering for each gate: the check, the cases it runs on, where it runs, what it measures, when it passes and what happens when it fails.

---

## When a soft gate fails

**Mitigation lever.** A way to ship with less risk while a Soft gate is reviewed. There are four: delay launch, beta label, feature flag and staged rollout.

**Delay launch.** The hard stop. The right call when a Hard gate fails.

**Beta label.** Launch with an "experimental" label to set expectations, and add the questions it gets wrong to your golden set.

**Feature flag.** Connect the feature to a live eval, so it switches itself off if the failure rate goes past your threshold.

**Staged rollout.** Launch to a small share of users first, such as 5%, and roll back if the eval score drops in production.

---

## Module 5: Run Evals on Live Traffic Across Product Lines

> Vocabulary for the cohort. Use this list when reviewing the [Module 5 deck](Module%205%20-%20Slides%20%28Shareable%29.html), the [Notes](Module%205%20-%20Notes%20%28Shareable%29.html) and the [Lab Guide](Module%205%20-%20Lab%20Guide.html).

---

## After launch

**Drift.** Model performance shifting as real-world data and user behavior change, while the model stays the same until it's retrained.

**Bias.** Outputs that skew unfairly toward certain groups. It can creep back in after launch, even if the product was fair before.

**Offline eval.** Your checks run on a fixed test set, such as the golden set, before you ship. It proves the product works on the cases you already know about.

**Online eval.** The same checks run on a sample of real traffic after launch. It tells you whether the product is still good once real people use it.

**Trace.** The record of everything that happened for one request: the question, each step the agent took, and the answer it gave.

**Sampling.** Choosing which live requests to score, because scoring every one costs too much: a random sample, more of the high-risk questions, and every request a cheap check flags.

**Drift monitor.** A check that compares the questions live users ask with the ones the product was built and tested on, and alerts when the mix moves.

**Periodic audit.** People reviewing a sample of high-risk answers on a set schedule, to catch bias and fairness problems only a person can judge.

**Error feed.** Live failures grouped by what went wrong, and ranked by how often they happen and how much they cost.

---

## Across product lines

**Coverage matrix.** A table of every AI product against the same five trust metrics, where each cell names the check that covers that risk, or shows a gap.

**Covered (✅).** A check runs on this risk regularly.

**Partial (⚠️).** Someone spot-checks the risk by hand, or the check only measures part of it.

**Gap (❌).** Nothing checks this risk.

**Accepted gap.** A gap you decide to live with for now, with the reason and what would make you change your mind.

**Critical gap.** The gap that would do the most damage if it failed tomorrow, and the one you close first.

**External product.** An AI product customers use directly. Its failures are visible right away and carry direct reputational risk.

**Internal product.** An AI product other teams and models use. Its failures spread into everything downstream and carry indirect systemic risk.

---

## The eval budget

**Eval budget.** The money and time a team can spend on evals: annotation, compute and release speed.

**Coverage, cost and velocity.** The three things an eval budget trades off. More coverage costs more and slows releases.

**Online eval (budget level).** An LLM judge or a reviewer scores live traffic continuously. The most expensive level.

**Periodic audit (budget level).** People review a sample of answers every week or two. About 10% of the online eval cost.

**Code-based check (budget level).** A quick rule check, or a spot-check on every release. About 5% of the online eval cost.

**Downgrade.** Covering a failure with a cheaper level than an online eval, with a clear note on what the cheaper check misses.

**80/20 rule.** Spend most of the team's time on targeted evals and error analysis, not on rebuilding basic infrastructure.

**Sampling cadence.** How often each check runs: light checks daily, exhaustive tests at release.

---

## Module 6: Make Evals the Way the Org Ships

Key terms introduced or sharpened in Module 6: **Make Evals the Way the Org Ships**.

---

**Adoption Risk** · The executive translation of the Hallucination Rate metric on the Trust KPI Dashboard. High hallucination rates predict user churn and loss of utility, a direct revenue signal leadership can act on.

**Answer (Pyramid)** · Tier 1 of the Pyramid Principle. The conclusion or specific recommendation stated in sentence one. Answers "so what?" upfront, even if the meeting is cut short, your strategic position is clear.

**Argument (Pyramid)** · Tier 2 of the Pyramid Principle. One of 3 to 4 distinct, mutually-exclusive logical pillars that support the Answer. Adoption Risk · Brand Risk · Legal Compliance · Reliability · Revenue.

**Bridge-builder** · The PM's role in a Hybrid trust-governance model. Operates the hub-and-spoke, leveraging central infrastructure while keeping the spoke focused on local product context.

**Centralized governance** · A trust-governance model for mature, high-regulation orgs. Trust is owned at the institutional level. PM role: guardian. Strategic rationale: compliance insurance, defensibility over speed.

**Champion's Cheat Sheet** · The canonical Pyramid Principle AI prompt introduced in M6. Used as a force-multiplier for high-stakes drafting, flips raw technical updates into executive memos. Baked into Lab 1 (M6 · Ship/Hold Memo Builder).

**Champion's Framing** · The "after" state of a high-stakes memo: Answer up front · arguments framed as business risk · evidence anchored in trust metrics · high-authority close with a specific ask and deadline.

**Closed-Loop Evaluation** · The 2026 eval operating model that ties the whole course together: offline eval → CI gate → production-trace eval → cluster failures (the Error Feed) → optimize → back through CI, all running on **one shared rubric vocabulary**. Championing responsible AI means institutionalizing this loop as how the org ships AI, not treating evals as a one-time launch gate. Anchored by Ankur Goyal (Braintrust): _"evals are the modern version of a PRD."_

**Compliance Readiness** · The executive translation of the Fairness metric on the Trust KPI Dashboard. Essential for regulatory and brand safety.

**Conformity Assessment** · A regulatory eval regime with teeth. For high-risk AI under the **EU AI Act**, "compliance" becomes an eval you actually _run_, documented eval evidence, a risk-management process, demonstrable human oversight, and logging/traceability of model behavior, rather than a vague business-impact category. The PM move: treat conformity as a hard eval gate in the Eval Playbook's Enforcement column.

**Consistency Debt** · The accepted cost of running a Decentralized trust-governance model. Different teams operate to different eval standards because the goal is finding product-market fit; consistency is sacrificed for innovation velocity.

**Data-First Trap** · A common PM mistake in high-stakes conversations. The PM has the right data but loses the room: vague intro, symptoms instead of diagnosis, buried recommendation, low-authority close. The "before" example in the M6 case study.

**Decentralized governance** · A trust-governance model for early-stage, low-regulation orgs. Trust is owned at the feature level. PM role: explorer. Strategic rationale: innovation velocity, accept "consistency debt."

**Discovery Loop** · The bottom-up half of the two-loop feedback system. Failure-spotting workshops with engineers, designers, and domain experts that surface real-world failure modes, codified into the Eval Playbook. DoorDash uses this for cross-functional incident reviews.

**Engagement Signal** · The executive translation of the UX Trust metric on the Trust KPI Dashboard. Measures how calibrated user trust actually is, directly connected to retention.

**Escalation Path** · The fifth component of the Eval Playbook. Defines the final judge who makes the call when a soft gate fails under launch pressure. Removes ambiguity in high-pressure moments.

**Eval Playbook** · A PM-owned document that serves as the single source of truth for AI quality. Five required components: Scope · Ownership · Enforcement · Frequency · Escalation Path. The "engine room" that makes the strategy real.

**Eval ROI** · The value of your eval _program_, measured in **outcomes**: incidents prevented, time-to-detection, ship confidence, and regression catch-rate, explicitly **not** in adoption or token usage. Per Meaghan Choi (Anthropic, ProductCon 2026): measure AI ROI beyond adoption and tokens. The framing that lets a PM defend eval-platform budget as a growth investment, not a cost center.

**EU AI Act** · The EU's risk-tiered AI regulation. For systems classed as **high-risk**, it mandates a documented eval/risk regime, human oversight, and logging/traceability, the legal backbone for treating compliance as a **Conformity Assessment** eval you run, not a box you check.

**Evidence (Pyramid)** · Tier 3 of the Pyramid Principle. Specific trust metrics, data, and results that prove each argument. The Trust Dashboard supplies the signal; the Pyramid gives the structure to weaponize the data.

**Explorer (PM role)** · The PM's mode in a Decentralized governance model. Drives velocity. Accepts that different teams may operate to different eval standards because the goal is finding product-market fit.

**Failure-Spotting Workshop** · A bottom-up activity in the Discovery Loop. Brings together engineers, designers, domain experts, and legal to hunt for failures before they hit production. Each function spots a different class of risk.

**Final Project Showcase** · The capstone activity of the AI Evals certification. Learners present their ship/hold decision (typically ~10 minutes per presenter) and submit individual deliverables to the learning platform within 7 days of course completion.

**Governance Loop** · The top-down half of the two-loop feedback system. Trust-review cadences and the Trust Dashboard that translate technical eval data into a leadership narrative. Outcome: defensible go/no-go decisions and resource allocation.

**Governance Mode** · The trust-governance model that defines your PM playbook: Decentralized · Hybrid · Centralized. Picking the wrong mode for your org's stage is one of the costliest cultural mistakes.

**Guardian (PM role)** · The PM's mode in a Centralized governance model. Works in a high-stakes environment where one failure can jeopardize the whole company. Uses Eval Gates as a defensibility shield.

**Holistic Safety Framework** · DeepMind's three-layer eval approach: model capabilities · risk of human misuse · long-term systemic impact. The PM takeaway: ownership means widening your lens beyond "Is the answer correct?"

**Horizontal Relationships (Pyramid)** · The Pyramid Principle property that each Argument is mutually exclusive, no overlap, no double-counting, no gaps in the case.

**Hub (Central · Execution)** · Owns the system integrity. Trust & Safety / AI Platform teams provide shared testing libraries, global safety standards, and the technical infrastructure to run evals at scale. Their job is to be an enabler, not a bottleneck.

**Hub-and-Spoke** · The organizational pattern matching the Hybrid governance model. Central hub provides shared infrastructure and standards; product team spokes own context-specific risk and decisions.

**Human Oversight** · A core requirement of any high-risk-AI conformity regime (and the EU AI Act): a human can meaningfully understand, monitor, and override the system's outputs. In eval terms, it is testable, a documented escalation path, a human-in-the-loop checkpoint on high-severity decisions, and proof the override actually works. Connects the M6 Escalation Path to regulatory teeth.

**Hybrid governance** · A trust-governance model for scaling, medium-regulation orgs. Trust is a shared responsibility. PM role: bridge-builder. Strategic rationale: balance central leverage with local context, too big for chaos, too fast for total central control.

**Leadership Pivot** · M6's mindset shift. The move from "the PM who runs the evals" to "the PM who owns the strategic narrative for product integrity." The validation pivot from tactical bug reporting to executive influence.

**learning platform Submission** · Required individual upload of the Final Project Deliverables to Product School's learning platform within 7 days of course completion. A cohort can build from a shared deck, but each member submits a copy individually to earn certification.

**Ownership vs Execution** · The accountability split at the heart of a culture of responsible AI. You can outsource the testing process (Execution → Hub). You can never outsource the moral and business responsibility for the model's behavior (Ownership → Product team).

**Pyramid Principle** · The Barbara-Minto communication framework. Top-down structure: Answer (the recommendation) → Arguments (3 to 4 mutually-exclusive pillars) → Evidence (specific trust metrics). M6's primary tool for high-stakes conversations.

**QBR (Quarterly Business Review)** · The first ritual the PM should hijack to insert the Trust Dashboard. Forces a conversation about Trust Debt with the same rigor as revenue.

**Reliability Risk** · The executive translation of the Robustness metric on the Trust KPI Dashboard. Measures how the model handles adversarial / edge cases.

**Responsible Scaling Policy (RSP)** · Anthropic's published commitment to delay deployment if safety evals flag catastrophic risks. The PM takeaway: leverage external validation as a political and professional shield to justify delaying a launch.

**Risk Translation** · The Senior PM skill of converting technical metrics into business language. Robustness 12% → "the Trust Debt our rivals are exploiting." A core requirement of the Pyramid Principle's Argument tier.

**Ship/Hold Decision** · The final ship/hold recommendation for the Ascend IQ case study, the deliverable for Slide 9 of the Final Project deck. Built in Lab 1 (M6 · Ship/Hold Memo Builder) using the Pyramid Principle.

**Spoke (Product Team · Ownership)** · Owns the contextual precision. Domain-specific failure modes, user risk profile, the final go/no-go decisions. The PM lives in the spoke and owns the moral and business responsibility for the model.

**System Integrity** · What the Central Hub owns. Shared testing libraries, global safety standards, and the technical infrastructure to run evals at scale.

**Trust Dashboard** · See Trust KPI Dashboard.

**Trust Debt** · The accumulated risk of shipping AI without adequate evaluation infrastructure. Surfaces in the Pyramid Principle as the "what we're losing if we don't act" framing.

**Trust Integrity** · The "new mandate" replacement for "feature delivery." The PM owns the trust integrity that allows the org to take bigger swings with confidence. _Trust is the speed of your organization._

**Trust KPI Dashboard** · The PM's control panel for leadership. Five metrics (Hallucination Rate · Fairness · Robustness · Latency · UX Trust), each with a target, owner, cadence, and executive meaning. Translates "model health" into "business health."

**Trust Moment** · An all-hands ritual the PM should hijack, celebrating an eval gate that successfully caught a critical risk before launch. Reframes safety as a win, not a delay.

**Trust as Infrastructure** · The mindset shift from "evals are a safety check at the end" to "evals are the substrate the org runs on." Frames trust as a growth engine and not a cost center.

**Trust Objective (OKR)** · A formal, measurable OKR aligned with trust outcomes (e.g. "Reduce hallucination rate by 50% by Q3"). Aligns team incentives so safety is a shared, rewarded responsibility alongside velocity.

**Trust Review Cadence** · A scheduled meeting (QBR or monthly trust review) where the Trust Dashboard is the primary artifact. The mechanism by which the Governance Loop runs.

**Two-Loop Feedback System** · The Discovery Loop (bottom-up) + the Governance Loop (top-down). Moves trust from a "department" to a "cadence" by connecting the engineer's desk to the CEO's office.

**Usability Signal** · The executive translation of the Latency metric on the Trust KPI Dashboard. Directly impacts retention and feature friction.

**Validation Pivot** · M6's strategic shift. Moving from checking compliance boxes to owning the strategic narrative of Product Integrity, the leadership posture that lets the PM weaponize Trust Metrics into high-stakes decisions.

**Vertical Relationships (Pyramid)** · The Pyramid Principle property that every metric in the Eval Playbook rolls up into a business argument that supports the Answer.

**VP-of-Product Critic Prompt** · The stranger-test prompt baked into Lab 2 (M6 · Final Pitch Prompt Generator). Has an LLM read your final pitch as a skeptical VP would: would-fund / would-not-fund verdict in three short paragraphs.

---

_End of Module 6 glossary · pair with M1 to M5 glossaries for the complete AI Evals vocabulary._

---
