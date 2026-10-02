# You Cannot Govern an Engineering Decision If Its Record Is Only a Story

## Most decision records explain what happened afterward. They do not show what was visible when the choice was made.

**Engineering Before Governance | 02 / 08**

[[M_EBG_A_02-0.png]]

An AI agent is asked to change the retry behavior of a payment client.

Its decision record looks reassuring. The agent considered two options, respected the idempotency and public API constraints, selected one bounded retry, and updated the code.

Then a reviewer asks a few simple questions:

- Which context fragments were actually sent to the LLM?
- Were both alternatives actually considered, or added later to complete the record?
- Did the agent receive the listed constraints before it selected an option?
- Is the rationale a captured explanation or a retrospective story?
- Did the decision that appeared during generation match the generated code?

The organization has a decision document. It does not yet have reliable evidence of decision behavior.

That is the governance problem:

> If a decision record mixes captured behavior with a story written afterward, governance cannot tell what actually happened during generation.

Before a decision can be governed, engineering must make the relevant behavior visible.

---

## 1. Governance Problem: A Decision Record Is Not Yet Decision Evidence

Look at almost any development workflow today and you will find plenty of material that looks like governance evidence: tickets, specifications, prompts, chat histories, pull requests, tool logs, approvals, test results, and Git commits.

So the problem is not that we have nothing.

The problem is that these artifacts answer different questions. A specification tells us what was intended. A commit tells us what changed. A tool trace may show that a file was read. A rationale explains a choice. An approval tells us that someone accepted a result.

Useful? Absolutely. But none of them, on its own, shows the full behavior of one decision.

Take `RULE-PAYMENT-IDEMPOTENCY@v4`. If it appears in the decision record, we know it was cited. We still do not know whether the agent received it before choosing, used it to compare the alternatives, or mentioned it afterward because the final code happened to comply.

Rationale has the same limitation. It helps a reviewer understand the stated reason for a choice, but it is not a window into the model's private reasoning. Research on chain-of-thought faithfulness has shown that a plausible explanation can leave out influences on the answer.

What we need is neither an abstract decision summary nor raw model telemetry such as token probabilities and confidence values. We need the observable parts of decision behavior to be made explicit: what went in, what options appeared, what constraints were used, what was selected, and what was actually implemented.

[[M_EBG_A_02-1.png]]

---

## 2. Existing Solutions Preserve Parts of the Decision

Fortunately, we do not need to invent everything from scratch.

Architecture Decision Records preserve context, a selected option, and consequences. They are valuable for long-lived architecture knowledge, but they usually summarize a decision rather than capture one decision event inside an agentic workflow.

W3C PROV models relationships among entities, activities, agents, usage, generation, and delegation. Decision provenance extends this thinking to inputs, decisions, actions, and effects. These models provide useful relationships, but an organization must still decide what needs to be observed for its governance question.

Agent telemetry can retain model requests, tool calls, files accessed, timing, and outputs. Assurance cases, review, and approval can connect claims to evidence and judgment.

Put them side by side and the division of labor becomes clearer:

```text
Decision documentation explains the choice
Provenance connects actors, activities, and artifacts
Telemetry captures selected events
Review evaluates claims against evidence
```

That gives us several useful pieces. What it does not yet give us is one clear, event-level view of an AI-assisted engineering decision.

---

## 3. What Existing Solutions Still Cannot Resolve

This is where an otherwise polished decision record starts to come apart: it often contains more than the generation actually did.

Start with the decision point. A pull request can contain dozens of small choices, yet the workflow rarely marks the moment when one choice became necessary or shows which later action depended on it.

The decision basis is just as easy to misread. A file may exist in the repository without ever being read. A rule may be available without being delivered. A conversation may have been summarized before the choice. Looking at today's repository cannot tell us what was actually present at that moment.

Alternatives are particularly easy to rewrite. A template that demands two options can encourage someone, or an AI, to invent a second option after the fact. If alternatives appeared during generation, record them. If they did not, do not add them merely to complete the template.

Rules have the same problem. A repository may contain hundreds of rules, but Development Evidence should not copy all of them into the record. It should record a rule only when that rule was actually triggered or used during the generation.

Context can also be overstated. A specification may be one hundred pages long while only three sections were sent to the LLM. Recording the full specification as input would make the evidence look complete while hiding what the model actually received.

That may sound like a documentation problem, but it is really an evidence problem. If the record expands beyond what actually happened, later governance begins from a reconstruction rather than from the development behavior itself.

---

## 4. Governance Scope and the Elements That Must Become Visible

To keep the problem manageable, let us narrow the lens. We are looking at one decision that occurs while an LLM generates a document or a piece of code.

The broader series calls the engineering representation needed for a governance judgment a **Governance Engineering Element**. Here, the specialized elements are **Decision Behavior Engineering Elements**, or DBEEs: the parts of the generation behavior that can be directly recorded and traced.

The rule for Development Evidence is simple:

> Record what was actually sent, what actually appeared during the decision, what actually triggered, and what was actually generated.

### Record the context actually sent

If an entire specification was supplied, record the specification and version. If only selected sections or retrieved chunks were supplied, record those sections or chunks.

Do not list every document available in the repository. Availability is not Development Evidence. The relevant evidence is the effective context used for this generation.

### Record alternatives only when they appear

If the generation produced three implementation options, record all three. If it moved directly to one solution, record that decision without inventing rejected alternatives.

The goal is not to force every decision into the same shape. It is to preserve the behavior that actually occurred.

### Record rules only when they trigger

If a rule is triggered during the decision, record the Rule ID, version, trigger, and the effect it had on the generated choice. If no rule is triggered, do not pad the record with every rule that might have been relevant.

For example, if `RULE-PAYMENT-IDEMPOTENCY@v4` causes the generation to reject a retry strategy that creates a new key, that trigger belongs in the evidence.

### Record the decision and generated result

Finally, connect the decision behavior to the document or code that was generated. The useful question is straightforward: what decision appeared during generation, and where did its result appear in the output?

[[M_EBG_A_02-2.png]]

---

## 5. Engineering the Decision Evidence

Once that behavior is visible, the engineering design becomes much easier to explain. We only need to keep three things separate:

```text
Decision behavior
    What occurred while the document or code was generated

Development Evidence
    The retained context, trigger, alternative, decision, or output event

Claim
    What someone says the evidence demonstrates
```

Consider the claim: "The idempotency rule was applied when the retry option was selected."

A document listing the rule supports only that it was cited. Stronger Development Evidence would show that the rule entered the supplied context, was triggered during generation, and changed or constrained the generated result.

From there, a few practical rules follow:

- give one bounded decision one stable Decision ID;
- record only the context fragments actually sent to the LLM;
- bind those context fragments, triggered rules, and generated artifacts to exact versions;
- capture the behavior while generation occurs instead of rebuilding it later;
- include alternatives only when they actually appear;
- include rules only when they actually trigger;
- connect each evidence item to the claim it supports;
- append corrections rather than silently rewriting the past;
- use a Trace ID to connect the supplied context, decision behavior, and generated artifact.

That capture layer is governance evidence infrastructure. Think of it as the plumbing that preserves what actually happened during generation for later review.

But having the plumbing is not the same as making the governance decision.

Engineering can make the supplied context, generated alternatives, triggered rules, decisions, and outputs visible. Evidence can support claims about them. Neither approves nor rejects the decision.

Governance begins later, when a governance process evaluates a claim using that evidence and decides what action follows.

```text
Engineering makes the decision behavior visible
Evidence preserves what can be supported
Audit evaluates the claims
Governance decides and acts
```

[[M_EBG_A_02-3.png]]

The Evidence Skill that motivated this article is one way to build that capture layer. Its job is intentionally narrow: faithfully record the supplied context, alternatives that appeared, rules that triggered, decisions that formed, and the document or code that was generated. It does not reveal hidden reasoning, and it does not try to answer every governance question.

That boundary makes the process repeatable:

```text
Plan: define where generation behavior can be captured
Do: record supplied context, decision events, and generated artifacts
Check: evaluate claims against evidence
Act: improve the generation or the capture mechanism
```

---

## 6. Example: One Retry Decision

Now we can return to the payment retry decision. The example records only what occurred while the code was generated.

```yaml
development_evidence:
  id: DEV-EVIDENCE-042
  trace_id: TRACE-payment-retry-184

generated_artifact:
  type: code
  ref: src/payment/client.ts@sha256:...

input_context:
  - ref: REQ-payment-retry-018@v2
    fragment: retry-temporary-failures
    evidence: EVT-context-101
  - ref: VSS-payment-system@v12
    fragment: system-design/payment-retry
    evidence: EVT-context-102
  - ref: src/payment/client.ts@sha256:...
    fragment: lines-118-176
    evidence: EVT-context-103
  - ref: RULE-PAYMENT-IDEMPOTENCY@v4
    fragment: preserve-existing-key
    evidence: EVT-context-104

decision_behavior:
  subject: Choose retry behavior for temporary payment failures
  alternatives:
    - Do not retry
    - Retry once with a new idempotency key
    - Retry once with the existing idempotency key
  triggered_rules:
    - ref: RULE-PAYMENT-IDEMPOTENCY@v4
      trigger: Candidate introduced a new key for the retry.
      effect: Candidate was rejected.
      evidence: EVT-rule-trigger-021
  decision: Retry once for temporary failures using the existing key
  evidence: EVT-decision-023

generation_result:
  change: Added one bounded retry and reused the existing key.
  evidence: EVT-code-generation-026
```

The record does not claim to know what happened inside the model. It shows the exact context fragments supplied, the alternatives that appeared, the rule that triggered, the decision that formed, and the code change that was generated.

The structure is intentionally conditional. If no alternatives appeared, the `alternatives` section is omitted. If no rule triggered, there is no `triggered_rules` section. If only three sections of a long document entered context, only those three sections are recorded.

Having this record does not mean the decision has been governed. It gives later governance a faithful account of the development behavior it can inspect.

> Evidence does not turn a story into truth. It tells governance which parts of the story the engineering system can actually support.

---

## References

- [W3C PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/)
- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [Decision Provenance: Harnessing Data Flow for Accountable Systems](https://www.repository.cam.ac.uk/items/14c68264-4c52-41d9-bf37-1dccc966cdcb)
- [Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting](https://proceedings.neurips.cc/paper_files/paper/2023/hash/ed3fea9033a80fea1376299fa7863f4a-Abstract.html)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
- [AWS Prescriptive Guidance: Using Architectural Decision Records](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/introduction.html)

### Related Work by the Author

- [Spark Tsai, *Runtime Governance vs. Development Governance: Why Runtime Interception Is Not Decision Behavior Governance*](https://doi.org/10.5281/zenodo.18876913)
- [Spark Tsai, *Toward Decision Behavior Governance: Governance Existence, Invocation, and Decision Formation*](https://doi.org/10.5281/zenodo.18876165)
- [Spark Tsai, *Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development*](https://doi.org/10.31224/6616)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
