# You Cannot Govern an Engineering Decision If Its Record Is Only a Story

## Most decision records describe a plausible decision after the fact, but do not prove what was observable when the decision was made

[[M_EBG_A_02-0.png]]

An AI agent is asked to modify the retry behavior of a payment client.

The resulting decision record looks reassuring. It says that the agent considered two retry strategies, applied the idempotency and public API constraints, selected one bounded retry, and changed the implementation.

But when a reviewer asks how the record was created, the answers become less certain:

- Which input artifacts and versions were available, delivered, and actually accessed before the decision?
- Were both alternatives actually evaluated during execution, or generated afterward to complete the template?
- Were the listed rules delivered to the agent, merely available in the repository, or inferred from the final output?
- Is the rationale an execution-time explanation or a retrospective narrative?
- Does the timestamp come from a captured event or an estimated sequence?
- Who made the decision: the requester, the agent, the workflow, an approver, or some combination of them?
- Does the stated impact describe an expected effect or a result that was later verified?
- Did the approved and executed result match the option that the record says was selected?

The organization has a decision document. It does not yet have reliable evidence of decision behavior.

That is the governance problem:

> If a decision record does not distinguish observed behavior from declared explanation, derived state, and verified outcome, governance cannot determine what happened, what is merely claimed, or what the evidence can actually support.

Before decision behavior can be governed, engineering must first make the relevant parts of that behavior observable.

---

## 1. Governance Problem: A Decision Record Is Not Yet Decision Evidence

Engineering organizations already retain many decision-related artifacts:

- tickets and change requests;
- specifications and architecture decision records;
- prompts and conversation histories;
- pull requests and review comments;
- tool calls and execution logs;
- approvals, test results, and changed engineering artifacts;
- model telemetry and token reports.

The problem is that these records answer different questions.

A specification can show the intended design. A Git commit can show the resulting change. A tool trace can show that a file was accessed. A rationale can show the explanation supplied by a human or agent. An approval can show that someone accepted a result.

None of these records automatically proves the complete behavior of the decision.

This creates an **Evidence-Claim Disconnect**: evidence is retained, but the organization has not defined which governance claim each item supports.

For example, finding a rule identifier in a decision document may support the claim that the rule was cited. It does not, by itself, prove that the rule was delivered before selection, interpreted correctly, or applied to reject a non-compliant option.

Likewise, a well-written rationale may explain why an option appears reasonable. It does not prove that the stated rationale faithfully represents the process that produced the choice. Research on chain-of-thought explanations has shown that model-generated explanations can be plausible while omitting influences on the answer. Governance should therefore evaluate retained engineering evidence, not treat generated reasoning as direct access to a model's internal process.

The goal is not to reproduce hidden cognition. The goal is to establish what the engineering system can legitimately observe and support.

[[M_EBG_A_02-1.png]]

---

## 2. Existing Solutions Preserve Parts of the Decision

Several established practices already contribute useful pieces.

Architecture Decision Records capture a decision, its context, and consequences. They are effective for preserving durable architectural knowledge, but their usual purpose is not to provide a complete event-level account of an agentic workflow.

W3C PROV provides a general model for describing entities, activities, agents, usage, generation, derivation, association, and delegation. It offers a strong foundation for expressing provenance relationships, but it does not decide which decision behavior an engineering governance problem requires.

Decision provenance extends provenance thinking to the relationships among inputs, decisions, actions, and their effects. This is close to the accountability problem, although an organization must still define the observable boundary of each individual engineering decision.

Logs and agent telemetry can preserve model requests, tool calls, files accessed, outputs, timing, and runtime identities. Those observations are important, but a log event does not explain its governance significance by itself.

Assurance cases, reviews, and approvals connect claims with supporting evidence and judgments. Yet they depend on engineering systems producing evidence that can be identified and evaluated in the first place.

These practices are complementary:

```text
Decision documentation
    preserves an explanation of a decision

Provenance
    relates entities, activities, agents, and derivations

Telemetry
    captures selected runtime events

Assurance and review
    evaluate claims against evidence
```

Together they provide valuable records. None, by itself, defines the complete observable boundary required to govern one AI-assisted engineering decision.

---

## 3. What Existing Solutions Still Cannot Resolve

Decision behavior becomes difficult to govern when several states collapse into one record.

### The decision point is unclear

A final artifact contains many choices, but the workflow may not identify when a choice became necessary, when it was made, or which action depended on it. A generated list of "important decisions" after completion is not equivalent to captured decision events.

### The actors and authorities are mixed together

A single `Author` field can hide multiple roles. A person may initiate the task, an agent may propose an option, a workflow rule may constrain selection, and another person may approve the result. Governance needs to know who or what performed each role, not only whose name appears on the document.

### The decision basis is implicit

Files may exist without having been read. Rules may be available without having been delivered. Conversation content may have been summarized or truncated. Without versioned references to the effective prompt and context, a later reviewer may inspect information that was not present when the decision occurred.

### Alternatives can be reconstructed fiction

A template that always requires two options encourages complete-looking comparisons. When only one path was actually available, the second option may be invented after the fact. When several alternatives were explored through tools or intermediate outputs, a compact narrative may omit them.

The record should allow `none observed`, `not captured`, and `unknown`. Absence is more governable than manufactured certainty.

### Constraints are listed but not connected to behavior

Recording `RULE-017` says little unless the organization can determine its version, whether it was applicable, whether it was available or delivered, how it affected evaluation, and whether compliance was later verified.

### Rationale is confused with evidence

A rationale is a declared explanation. It is valuable, but its evidential status differs from an execution event, an input artifact, or an independently verified result. Treating all four as equivalent produces false confidence.

### Impact is predicted rather than verified

Decision records often describe what a choice "will" improve. Governance also needs the resulting engineering action, affected artifact, consistency verification, and any divergence from the selected option. Otherwise the record ends at intention and never shows whether this decision was actually realized.

### Time and sequence are approximate

Estimated timestamps can make a record appear precise while obscuring that no event was captured. For governance, event order may matter more than decorative precision: was a rule supplied before the choice, was approval obtained before implementation, and was verification completed before acceptance?

These are not documentation-quality problems. They determine whether an organization can review responsibility, detect control failure, reproduce the decision basis, and improve the workflow.

---

## 4. Governance Scope and the Elements That Must Become Visible

The previous article argued that engineering must create the state governance evaluates. This requires a unit more precise than "the information we should keep."

A **Governance Engineering Element**, or GEE, is:

> An identifiable engineering representation required to make a governance condition observable, evaluable, controllable, reviewable, auditable, or improvable.

The definition starts from a Governance Problem. It does not prescribe one universal record containing everything.

```text
Governance Problem
    -> Governance Claim
    -> Required Governance Engineering Elements
    -> Evidence
    -> Evaluation
    -> Governance Action
    -> Improvement
```

For decision behavior, the specialized elements are **Decision Behavior Engineering Elements**, or DBEEs:

> Identifiable engineering representations required to make engineering decision behavior observable, recordable, traceable, and evaluable.

A DBEE is not a factor assumed to cause a decision. It is an element that governance needs to identify about the behavior surrounding a decision.

---

### One record must represent one decision event

The unit of governance in this article is not the complete design of a system, an entire specification, or a summary of all decisions made during a development run.

It is one identifiable engineering decision event:

> At a specific decision point, given identifiable inputs and constraints, an authorized human, agent, or workflow evaluates one or more available paths and selects a course of engineering action.

Examples include choosing whether to retry a failed payment request, selecting the shape of one API response, deciding where one validation rule belongs, or determining whether one database change requires a migration.

A specification may contain hundreds of such decisions. An ADR may summarize a significant one. A pull request may contain several. For Decision Behavior Evidence, each record needs a stable Decision ID and a bounded subject so that its inputs, constraints, alternatives, selection, realization, and evidence do not become mixed with other decisions.

---

### A single decision must be observable before, during, and after selection

The exact DBEE set depends on the Governance Problem. But a governable decision record must cover three observation windows. Recording only the selected option captures a conclusion without its basis or its actual consequence.

```text
Decision Input Snapshot
    -> Constraints and Authority
    -> Alternatives
    -> Evaluation
    -> Declared Selection
    -> Approval or Override
    -> Realized Decision
    -> Consistency Verification
    -> Trace
```

[[M_EBG_A_02-2.png]]

### Before the decision: input, constraints, and authority

Governance first needs the point-in-time basis from which the decision could be made:

- decision request, problem, subject, and triggering event;
- current state known before the decision;
- Prompt Artifact ID and version;
- Context Manifest and execution version;
- Change Scope and relevant system specification version;
- input artifacts and their versions;
- whether each input was available, delivered, accessed, or missing;
- applicable rules, constraints, and evaluation criteria;
- assumptions, unknowns, and unresolved input conflicts;
- requester, decision authority, delegated authority, and approval threshold.

These elements answer more than "what files existed?" A repository may contain a rule that was never delivered to the agent. An artifact may have been delivered but never accessed. A constraint may have been cited without being applied. These are different observable states and must not be collapsed into one `Input Artifacts` list.

Pre-decision observability establishes what the human, agent, or workflow was allowed and equipped to decide. It does not claim access to private model reasoning.

### During the decision: alternatives, evaluation, and selection transparency

Governance then needs to observe how the decision was formed at the level the engineering system can support:

- Decision ID, version, point, stage, run, event time, and Trace ID;
- proposer, evaluator, selector, and their identities;
- candidates actually observed during execution;
- source and formation event of each candidate;
- criteria and constraints applied to each candidate;
- supporting or conflicting evidence used in evaluation;
- rejected, deferred, or escalated candidates;
- selected option and selection event;
- declared rationale, its author, and capture time;
- expected impact, uncertainty, exception, override, or dissent.

Candidates should be recorded only when supported. A required template shape must not create alternatives that were never observed. Likewise, a rationale is a declaration associated with the selection, not proof of hidden cognition.

This window provides **decision transparency**: which alternatives were visible, how constraints related to them, what was selected, what impact was expected, and how the selection traces back to its basis.

### After selection: realized decision and consistency verification

A declared selection is not necessarily the decision that is realized in the engineering artifact.

An approver may modify it. A development control may block it. An engineer or agent may implement only part of it. The resulting specification, design, or code may also diverge from the selected option.

The post-selection observation remains inside the development stage and inside the boundary of this single decision. It needs:

- approval, rejection, modification, escalation, or override event;
- final authority responsible for the outcome;
- realized decision, including differences from the declared selection;
- engineering action actually authorized and performed;
- specification, design, code, or test artifact actually changed;
- expected engineering effect compared with the resulting artifact state;
- review or test used to verify that the artifact realizes the selected option;
- correction or rework when selection and realization diverge;
- complete trace from the input snapshot to the changed artifact.

This distinction produces three states that must remain separate:

```text
Declared Selection
    What the selector said should be chosen

Authorized Decision
    What the applicable authority allowed to proceed

Realized Decision
    What was actually written into the specification, design, or code
```

Only by connecting all three can governance determine whether this individual decision was followed, altered, blocked, or incorrectly realized. Deployment and production behavior may provide evidence for other governance problems, but they are outside the scope of this decision record.

### Evidence quality

- evidence item ID, source, and location;
- capture method and capture time;
- version or integrity hash;
- retention and access classification;
- relationship to the DBEE and governance claim;
- evidence status: `observed`, `declared`, `derived`, or `verified`;
- confidence, limitations, and `unknown` where appropriate.

Evidence quality is itself part of governability. A field without provenance may be data, but it is weak evidence.

---

## 5. Engineering the Decision Evidence

These terms should not be collapsed.

```text
Decision Behavior Engineering Element
    What governance needs to identify about decision behavior

Engineering Decision Behavior Evidence
    A retained item that supports a point-in-time state of that element

Governance Claim
    A statement made about the element using that evidence

Governance Judgment
    An evaluation of the claim under an applicable rule
```

Consider an `Applied Constraint` element.

The claim might be:

> Security rule `SEC-017` was applied when the architecture option was selected.

A decision document that lists `SEC-017` supports only that the rule was declared or cited. Stronger evidence may include a versioned context record showing the rule was delivered before selection, an evaluation event connecting the rule to each candidate, and an independent review confirming that the chosen result complies with it.

The evidence does not need to be equally strong for every decision. It needs to be explicit enough that governance can distinguish what is supported from what is assumed.

### Engineering rules for a decision evidence record

The record should be designed around several rules:

- one Decision ID represents one bounded decision subject;
- inputs, constraints, alternatives, selections, and realizations use stable IDs and versions;
- events are captured when they occur rather than reconstructed only after completion;
- initiator, proposer, selector, approver, executor, and recorder remain separate roles;
- every evidence item identifies its source, capture method, time, integrity reference, and related DBEE;
- `observed`, `declared`, `derived`, and `verified` remain different evidence states;
- `unknown`, `not captured`, and `none observed` are valid values;
- corrections create a new version or linked event instead of silently rewriting the past;
- Trace IDs connect the single decision to its input snapshot and resulting engineering artifact.

Adding these fields to a document after the work is complete is not enough. The development environment must capture observable events and stable references while the decision occurs.

This is the role of **Governance Evidence Infrastructure**:

```text
Governance Engineering Architecture
    organizes the elements required by governance problems

Governance Evidence Infrastructure
    captures, preserves, and connects supporting evidence

Decision Behavior Engineering Elements
    define what must be observable about one decision

Engineering Decision Behavior Evidence
    supports claims about those elements at a specific point in time
```

### Infrastructure is not governance

Creating observable elements does not mean that governance has occurred. Capturing evidence does not mean that a decision has been governed.

Engineering can establish the decision boundary, preserve the input state, identify roles, record alternatives, connect constraints to evaluation events, and trace a selection to its realized artifact. These capabilities make the decision governable. They do not determine whether the decision is acceptable.

Evidence has the same boundary. An event record may support the claim that a rule was delivered. A review may support the claim that the realized code matches the authorized decision. Neither item approves, rejects, escalates, or corrects the decision by itself.

Governance still requires:

- a governance claim to evaluate;
- applicable policy, rule, or acceptance criteria;
- an authorized governance role;
- an evaluation of evidence strength and limitations;
- a judgment such as accept, reject, request correction, or escalate;
- a control or improvement action based on that judgment.

The relationship is therefore:

```text
Engineering
    creates observable and traceable decision state

Evidence
    supports claims about that state

Governance
    evaluates those claims under rules and authority, then acts
```

Governance Engineering Elements and Governance Evidence Infrastructure are necessary foundations for governance. They are not substitutes for governance.

This is what **Engineering Before Governance** means: governance cannot evaluate what engineering has not first made identifiable and observable. Engineering comes first as infrastructure, but governance remains a separate act of judgment and control.

[[M_EBG_A_02-3.png]]

The Evidence Skill that motivated this article is one implementation direction for that infrastructure. Its scope is deliberately limited. It does not provide evidence for every governance question, and it does not reveal an agent's hidden reasoning. It captures evidence about identifiable engineering decision behavior: inputs, roles, alternatives, constraints, selection, realization, traceability, and verification.

With those elements engineered, the organization can apply a repeatable loop:

```text
Plan
    Define the elements and evidence strength required for this decision type

Do
    Capture the point-in-time decision events and artifact versions

Check
    Evaluate governance claims against the evidence that supports them

Act
    Correct missing instrumentation, authority gaps, or decision controls
```

---

## 6. Example: One Retry Decision

The following condensed template is not a universal schema. It demonstrates how a record can organize DBEEs while preserving the status of its evidence.

```yaml
decision:
  id: CODE-DEC-042
  version: 1
  subject: Choose retry behavior for transient payment failures

trace:
  run_id: RUN-payment-184
  scope_id: SCOPE-payment-retry-v2
  prompt_artifact: PROMPT-payment-retry-v3
  context_manifest: CTX-RUN-payment-184-v1

before_decision:
  request:
    ref: REQ-payment-retry-018@v2
    current_state: Payment client does not retry transient failures
    trigger_event: EVT-184
  roles_and_authority:
    initiator: human:Spark-Tsai
    decision_authority: agent:payment-dev-agent-v4
    approval_authority: human:payment-maintainer
    authority_rule: AUTH-CODE-REVIEW-002@v3
  inputs:
    - ref: src/payment/client.ts@sha256:...
      available: verified
      delivered: observed
      accessed: observed
      evidence: [EVT-context-delivery-087, EVT-file-read-311]
  constraints:
    - ref: RULE-PAYMENT-IDEMPOTENCY@v4
      applicable: verified
      delivered: observed
      evidence: EVT-context-delivery-088
    - ref: RULE-PUBLIC-API-STABILITY@v2
      applicable: verified
      delivered: observed
      evidence: EVT-context-delivery-089
  assumptions:
    - text: The payment provider classifies retryable failures explicitly
      status: declared

during_decision:
  decision_point:
    stage: edit-payment-client
    observed_at: 2026-04-29T00:00:40Z
    event: EVT-decision-point-020
  candidates:
    - name: Do not retry
      status: observed
      evidence: EVT-candidate-021
    - name: Retry once for explicitly transient failures
      status: observed
      evidence: EVT-candidate-022
  evaluation:
    - rule: RULE-PAYMENT-IDEMPOTENCY@v4
      candidate: Retry once for explicitly transient failures
      effect: allowed only when the existing idempotency key is preserved
      status: derived
      evidence: EVT-evaluation-024
  declared_selection:
    selected: Retry once for explicitly transient failures
    selector: agent:payment-dev-agent-v4
    event: EVT-selection-023
    expected_engineering_effect: One bounded retry without a public API change
    declared_rationale:
      text: Handles temporary provider failure while preserving idempotency.
      status: declared

after_decision:
  authorization:
    approver: human:payment-maintainer
    outcome: approved-with-condition
    event: EVT-approval-025
  realized_decision:
    value: One retry for retryable provider errors using the existing idempotency key
    differs_from_declared_selection: false
    evidence: EVT-code-change-026
  engineering_action:
    action: Updated payment client retry branch
    output_ref: src/payment/client.ts@sha256:...
    evidence: EVT-artifact-write-319
  verification:
    method: code review and focused retry tests
    result: implementation matches the authorized decision
    reviewer: human:payment-maintainer
    evidence: [REVIEW-2026-041, TEST-payment-retry-088]
  divergence:
    status: none-observed

limitations:
  - No claim is made about the model's private reasoning.
  - The declared rationale has not been established as causally faithful.
```

This template corrects several common weaknesses.

It separates pre-decision inputs and constraints from the behavior that occurs during selection. It distinguishes inputs that were available, delivered, and accessed. It records observed candidates instead of forcing exactly two. It then separates declared selection, authorization, realized decision, engineering action, and consistency verification. Most importantly, it exposes whether this one decision was realized differently from what was originally selected.

The same structure also makes missing evidence visible. If candidate generation was not captured, the record can say `not captured`. If the selector cannot be identified, it can say `unknown`. That is a governance signal, not a formatting failure.

The completed template is still not the governance result. It is an engineering interface for connecting one decision event to the evidence that supports it. A governance judgment occurs when an authorized role evaluates a claim against that evidence and decides what action follows.

> Engineering Decision Behavior Evidence does not reproduce hidden reasoning. It supports claims about identifiable Decision Behavior Engineering Elements at a specific point in time.

Having engineered the elements does not mean the decision has been governed. Having evidence does not mean governance has been completed. Both provide the infrastructure without which repeatable governance cannot operate.

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
