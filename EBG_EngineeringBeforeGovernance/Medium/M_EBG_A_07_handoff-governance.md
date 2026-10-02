# You Cannot Govern a Handoff If Responsibility and Context Change in Transit

## Three development handoffs expose a gap between workflow control and accountable human work.

**Engineering Before Governance | 07 / 08**

[[M_EBG_A_07-0.png]]

An engineer asks an AI agent to change the retry behavior of a payment client. The agent hands a design to a coding agent. The coding agent changes the code and sends a pull request to a human reviewer.

The ticket, code, and summary all arrive. But did the engineer give the first agent enough context and bounded authority? Did the next agent receive only what it needs, without inheriting a role or responsibility by default? And can the human reviewer actually perform the assigned review with the information provided?

That is the governance problem:

> If a development handoff does not make the transferred context, boundary, role, authority, evidence, and continuing responsibility visible for its direction, work can continue while governance loses continuity and accountability.

Before a handoff can be governed, engineering must make the transfer and the receiver's ability to continue visible.

---

## 1. Governance Problem: A Handoff Can Look Complete While the Work Is Not Continuable

Development work moves between people and agents, then between specialist agents, and often returns to a person for review. Much governance discussion focuses on agent workflow design: routing, constraints, monitoring, and AI accountability. Those matter, but the human-AI handoffs can remain underspecified: what information each side must provide, what the receiver is responsible for, and whether they have enough context and authority to do it.

Most teams can point to a transfer event: a ticket assignment, prompt, pull request, document, chat message, workflow transition, or agent protocol message.

But a transfer event alone does not answer:

- What did the sender actually provide, and what did the receiver actually receive?
- Which Scope, system view, and Rule versions applied at that boundary?
- Which decisions are established, and which remain open?
- Which Evidence supports the claims in the transferred summary?
- What action and decision authority does the receiver have?
- Who remains responsible for unresolved questions and risks?
- Did the next actor confirm readiness, or did the workflow simply move on?

An output can be correct and still be hard to continue safely. A vague task can expand an agent's authority by inference; a broad history can pass stale context to another agent; an unresolved risk can lose its owner. At the human end, a code diff supports code review, but not necessarily an audit of why the design was chosen or whether its residual risk is acceptable. The review a person can perform is bounded by what the handoff provides.

This is a governance gap, not merely a workflow defect. A workflow may successfully route a task, record that an agent completed it, and pause for a human. Yet none of those events shows that the next actor had the information, authority, and capacity required for the responsibility assigned. The process can look orderly while accountability becomes thinner at each transition.

[[M_EBG_A_07-1.png]]

---

## 2. Existing Solutions Handle Routing, Context, and Oversight in Different Ways

We already use many ways to pass development work forward.

Tickets, specifications, and prompts can define work; pull requests carry diffs, checks, and review decisions; Git preserves source history. These help route tasks and present generated work, but do not guarantee that the receiver got the context or evidence needed for the assigned responsibility.

Agent frameworks add explicit agent-to-agent control transfer. The OpenAI Agents SDK supports structured handoff input and filters; its documentation notes that prior conversation may be passed unless deliberately filtered, and compaction is not redaction.

The Agent2Agent protocol standardizes messages, tasks, context identifiers, status, and artifacts across systems. It does not itself define a development task's Scope, authority, or accountability.

Workflow frameworks such as LangGraph can checkpoint state and pause for human review. That supports resumption, but does not define what the person must judge or whether the review material is sufficient.

HITL patterns add a person at review or approval points. The checkpoint alone does not establish a clear duty, sufficient information, or a meaningful path to reject or escalate.

Provenance models such as W3C PROV help connect agents, activities, inputs, outputs, and delegation.

Each mechanism answers a useful but narrower question: Was work assigned? Did control move? Was state checkpointed? Which activity used or generated an artifact? These records are valuable, but they do not automatically answer whether a particular receiver had enough relevant context to continue or whether a human could verify the claim they were asked to judge. The gap is between recording that a handoff occurred and establishing that the work was continuable.

Together, existing tools address important mechanics:

```text
Tickets and pull requests route work between people and teams
Task prompts define what a human asks an agent to do
Agent protocols exchange tasks, messages, status, and artifacts
Workflow checkpoints preserve resumable execution state
HITL patterns place humans at review or approval points
Provenance links agents, activities, inputs, outputs, and delegation
```

The gap is not the absence of workflow tools. It is whether the transfer gives the receiver the right state, a clear responsibility, and evidence to support accountability.

---

## 3. What the Three Handoff Directions Still Leave Unresolved

### H2A: Did the agent receive enough information and a clear boundary?

"Fix the payment retry behavior" may omit the relevant system context, Scope, Rule, or escalation conditions. The agent needs the effective instruction and the context actually delivered, not merely a prompt-sent event. This connects to the earlier articles: 02 records decision behavior Evidence; 03 identifies elements through Trace IDs; 04 makes Prompt, Context, VSS, and Scope visible; 05 covers Rules; and 06 connects decisions to Impact Analysis and Decision Risk. The handoff is where the applicable elements must reach the agent in usable form.

### A2A: Did context spread, responsibility move, or roles carry over by default?

A broad history can pass stale, irrelevant, or sensitive context; a short summary can omit the constraint behind a decision. Meanwhile, the first agent may assume the next will verify a design, and the next may assume the requirements were already established. Unless roles and open-item owners are explicit, context travels more reliably than accountability. Access to an architect's analysis does not make an implementation agent an architect or grant it authority to accept risk.

### A2H: Is the human's responsibility clear, and is the response sufficient?

HITL identifies where a person appears; governance must define what they are expected and authorized to judge. A diff may support code review against a requirement. To audit decision risk, the response must also provide the Decision Analysis, alternatives, assumptions, Impact Analysis, risk, and supporting Evidence. Otherwise, “approve” asks the human to decide more than the handoff lets them inspect. In every direction, the record should show what was sent and received, what changed, and who owns what remains open.

[[M_EBG_A_07-2.png]]

---

## 4. Scope: Three Directions, Three Sets of Engineering Elements

The scope is software development: requirements, design, code generation, and review, not post-deployment operations.

The shared governance object is a **Handoff**: an identified transition where one actor's work state becomes another actor's input. But the elements that must be visible depend on its direction.

| Direction | What must be made visible before work continues |
| --- | --- |
| **H2A** | Actual instruction and delivered context; outcome and Scope; exclusions, authority, and escalation conditions. Apply the relevant series elements: Evidence (02), Trace IDs (03), Prompt/Context/VSS/Scope (04), Rules (05), Decision Risk (06). |
| **A2A** | The actual payload sent and received; why each context element is relevant; the receiving agent's assigned role and capability; decisions versus assumptions; unresolved questions and their accountable owner. |
| **A2H** | The human's specific review or decision duty; the artifact and supporting Evidence needed for it; alternatives, limitations, uncertainty, and open risks; the human's authority, access, and ability to reject, return, or escalate. |

HITL becomes meaningful when the human's duty is defined and the package matches it: code review needs a diff and checks; decision-risk audit needs decision analysis, alternatives, impact, risk, and Evidence.

### Shared Handoff Elements

Across directions, a handoff can be represented through a small set of linked elements:

- **Handoff ID and actors:** link the sending and receiving operations; identify roles when they affect responsibility or authority.
- **Payload and state:** record what was sent and received, with Trace IDs to the relevant Scope, VSS, Rule, artifact, decision, risk, and Evidence. A summary does not replace its supporting Evidence.
- **Authority and ownership:** state the receiver's permitted next action and who retains unresolved items.
- **Transition Evidence:** distinguish sent, received, assessed, accepted, returned, and subsequent action.

The package should be sufficient for the next task, not a conversation dump. Linked IDs form the trace chain; they make the transition inspectable, but do not decide whether work may continue.

So what are we governing? Not the mere existence of a prompt, message, or approval button. We are governing the conditions at the boundary: the fit between the work being transferred, the information actually received, the receiver's role and authority, and the responsibility that continues after the transfer. The required package is therefore task-specific. A coding agent and a risk reviewer should not receive identical material simply because they are part of the same workflow.

---

## 5. Engineering the Transfer Before Calling It Governance

For each boundary, define the next activity, what its receiver must know and may do, and which responsibility remains with them. Then capture the actual transfer.

For **H2A**, preserve the effective instruction and context actually delivered (02/04), link elements by Trace ID (03), and include relevant Rules (05) and decision-risk basis (06). Make Scope, exclusions, authority, and escalation explicit so later review can distinguish human-provided information from agent inference.

For **A2A**, define the receiver's task-specific role; record the actual payload and source Trace IDs; distinguish decisions from assumptions; and retain an owner for each open item. If context was filtered or summarized, preserve enough provenance to see what informed the next step.

For **A2H**, match the response to the duty. Code review needs the diff, relevant Scope and Rule, and test Evidence. Decision-risk audit needs Decision Analysis, alternatives, assumptions, Impact Analysis, controls, residual risk, and linked Evidence. Confirm the human has authority and access to reject, return, or escalate.

The trace chain should distinguish these events rather than collapse them into “handoff complete”:

```text
prepared -> sent -> received -> accessible -> assessed -> accepted / returned
```

Link these events to the handoff, operations, payload, state references, and supporting Evidence. Record versions, timestamps, roles, and status as needed to identify the state. Receipt proves delivery or access; acceptance records a response. Neither proves the decision was sound.

Before continuation, compare the assigned next action with the package and the receiver. Can the agent access the referenced Scope and Rule? Does the human have the artifact and evidence needed for the assigned review? Is the receiver authorized to take the next action, and is each open risk still owned? If a required condition is missing, the system should be able to mark the handoff incomplete, return it, or route it to someone with the right authority. This is the engineering design that makes a governance judgment possible; it does not automate the judgment itself.

Audit can now ask:

```text
H2A: Was the agent given enough verified context, a bounded task, and only suitable authority?
A2A: What context crossed the boundary, what was omitted, and who owns open decisions?
A2H: What exactly must the human decide, and can the human verify it with the supplied Evidence?
All: What was sent, received, changed, accepted, returned, and by whom?
```

Engineering makes the transition visible; Audit compares it with requirements; Governance decides whether and how work may continue. That is PDCA:

```text
Plan: define the readiness and responsibility conditions for each direction
Do: capture the actual payload, receiver state, and transition events
Check: test continuity, authority, sufficiency, and accountability against Evidence
Act: continue, return, reroute, correct, or improve the handoff design
```

---

## 6. Example: One Payment Change, Three Different Handoffs

Consider a payment retry change moving from an engineer to an analysis agent, then an implementation agent, and finally a human reviewer.

```yaml
handoff_chain:
  - handoff_id: H2A-PAYMENT-184
    direction: H2A
    from: { actor: engineer-17, role: payment-maintainer }
    to: { actor: analysis-agent-2, assigned_role: change-analyst }
    actual_input: "Analyze retry behavior; propose a bounded change. Do not edit files."
    context_refs: [SCOPE-PAYMENT-RETRY@v4, VSS-PAYMENT@v12, RTM-REQ-018@v2, RULE-IDEMPOTENCY@v4]
    authority: [read-repository, propose-design]
    exclusions: [edit-code, approve-risk]
    unresolved_owner: engineer-17
    receipt_evidence: EVD-H2A-RECEIPT-184

  - handoff_id: A2A-PAYMENT-185
    direction: A2A
    from: { actor: analysis-agent-2, role: change-analyst }
    to: { actor: coding-agent-5, assigned_role: implement-approved-design }
    actual_payload_refs: [DESIGN-PAYMENT-042@v1, DECISION-EXEC-042, RULE-IDEMPOTENCY@v4]
    not_inherited: [change-analyst-role, approve-risk-authority]
    open_item: "Confirm shared-boundary impact before merge"
    open_item_owner: engineer-17
    authority: [edit-scoped-files, run-listed-tests]
    receipt_evidence: EVD-A2A-RECEIPT-185

  - handoff_id: A2H-PAYMENT-186
    direction: A2H
    from: { actor: coding-agent-5, role: implement-approved-design }
    to: { actor: reviewer-9, assigned_role: verify-payment-change }
    artifact_refs: [src/payment/client.ts@git:8f2a1c7]
    diff_ref: PR-PAYMENT-RETRY-186
    evidence_refs: [EVD-GENERATION-026, TEST-PAYMENT-031, EVD-BOUNDARY-DIFF-186]
    human_duty:
      - review the code against Scope and idempotency Rule
      - audit whether the retry design's shared-boundary risk is adequately analyzed
    decision_audit_refs: [DECISION-ANALYSIS-042@v1, EVD-ALTERNATIVES-042,
      IMPACT-PAYMENT-042, RISK-PAYMENT-BOUNDARY-003@v2, EVD-RISK-CONTROL-042]
    authority: [review-code, audit-decision-risk, reject, return, escalate]
    known_limitation: "Agent did not determine whether residual business risk is acceptable"
    unresolved_owner: engineer-17
```

[[M_EBG_A_07-3.png]]

The first transfer gives the agent a bounded analysis task and leaves unresolved business questions with the engineer.

The implementation agent receives the approved design, not the analyst's role or authority. It can edit within Scope and run tests, while the shared-boundary question remains with its named owner.

The reviewer can inspect code because the package includes a diff, Scope, Rule, and test Evidence. The Decision Analysis, alternatives, Impact Analysis, and residual-risk records also let them audit why the design was chosen. With only the diff, they could review the implementation but could not claim to have audited the decision risk. That is a mismatch between assigned duty and supplied information, not a failure of the human.

Trace IDs connect the requirement, Scope, system view, Rule, decision, artifacts, Evidence, and handoffs. Audit can reconstruct what each actor received, what authority applied, and who owned open items. Governance still judges the evidence and authorizes the next stage.

Different transitions need different packages. What they share is this: capture the real transfer, define the receiver's duty and authority, preserve open-item ownership, and record what happened next.

> Handoff engineering does not govern the decision. It makes continuity, responsibility, and evidence visible enough for governance to judge.

---

## References

- [OpenAI Agents SDK for Python: Handoffs](https://openai.github.io/openai-agents-python/handoffs/)
- [A2A Protocol: Specification](https://a2a-protocol.org/dev/specification/)
- [LangGraph: Thinking in LangGraph](https://docs.langchain.com/oss/javascript/langgraph/thinking-in-langgraph)
- [W3C PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/)
- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)

### Earlier Articles in This Series

- [02: Decision Behavior Evidence](M_EBG_A_02_decision-behavior-evidence.md)
- [03: Trace ID, Role, Version, and Timestamp](M_EBG_A_03_trace-role-version-timestamp.md)
- [04: Prompt and Context Governance](M_EBG_A_04_prompt-context-governance.md)
- [05: Rule Governance](M_EBG_A_05_rule-governance.md)
- [06: Decision Risk Control](M_EBG_A_06_decision-risk-control.md)

### Related Work by the Author

- [Spark Tsai, *Beyond HITL: Continuation Readiness as a Governance Requirement for Enterprise AI Workflows*](https://doi.org/10.5281/zenodo.21856291)
- [Spark Tsai, *Anchor Architecture: A Minimal Structural Foundation for Software Traceability in AI-Assisted Software Development*](https://doi.org/10.31224/6580)
- [Spark Tsai, *Viewpoint-Structured Specification (VSS)*](https://doi.org/10.31224/6612)
- [Spark Tsai, *Decision Risk: A Structural Governance Framework for AI-Assisted Software Development*](https://doi.org/10.5281/zenodo.19025533)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
