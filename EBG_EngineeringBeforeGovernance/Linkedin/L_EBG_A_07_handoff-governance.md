# A Human Approved the AI Change. Did They Have Enough to Judge It?

**Engineering Before Governance | 07 / 08**

"A human makes the final decision."

That can provide valuable oversight. It can also assign someone a responsibility the handoff leaves them unable to perform.

A reviewer who receives a diff and passing tests can inspect implementation. If asked to approve the decision's architecture impact and residual business risk, they need additional analysis and authority.

The approval checkpoint is visible. The conditions for meaningful review may still be missing.

[[L_EBG_A_07-0.png]]

## Work can arrive while accountability becomes unclear

Consider a payment retry change moving from an engineer to an analysis agent, then to a coding agent, and finally to a human reviewer.

The first agent receives a vague request. The coding agent receives a short design summary. The reviewer receives the pull request.

The workflow completes every transfer. But who owns the unresolved transaction-boundary question? Which constraints reached the coding agent? What exactly is the human expected to judge?

Tickets, prompts, protocols, checkpoints, and pull requests support routing and continuity of execution. A transfer event alone does not establish that the receiver has the information, access, authority, and capacity required for the next task.

## Three handoff directions require different packages

**Human to agent (H2A).** The agent needs the actual instruction, delivered context, expected outcome, approved Scope, applicable rules, exclusions, and escalation conditions. A human asking for analysis should make clear whether editing code is authorized.

[[L_EBG_A_07-1.png]]

**Agent to agent (A2A).** The receiving agent needs relevant payload, source references, an assigned role, and a clear separation between established decisions and unresolved assumptions. Access to an analyst's output does not grant the coding agent the analyst's role or authority to accept risk.

**Agent to human (A2H).** The human needs a specific duty and material that supports it. Code review needs the diff, requirements, scope, rules, and verification. Decision-risk review may also need alternatives, assumptions, Decision Analysis, Impact Analysis, controls, and residual risk.

In all three directions, unresolved items need named owners. A conversation summary should not become the place where responsibility silently disappears.

[[L_EBG_A_07-2.png]]

## Capture what crossed the boundary

Give the handoff an identity and connect it to the sending and receiving activities. Record the actual payload sent and received, with versioned references to the relevant decisions, artifacts, scope, rules, risk, and evidence.

Record filtering and summarization when observable. A full history can carry stale or irrelevant context. A short summary can omit a constraint. The appropriate package depends on the receiver's task.

Preserve the distinction between prepared, sent, received, accessible, assessed, accepted, and returned. A sent reference may be inaccessible to the receiver. Receipt establishes a transfer; acceptance records a response. Neither alone establishes that the next decision was sound.

Before continuing, compare the package with the assigned responsibility. Can the receiver resolve the references? Is the permitted next action clear? Does every open question still have an owner? Can a human return or escalate the work when the evidence is insufficient?

These conditions make readiness inspectable.

## One change, three concrete boundaries

The engineer asks an analysis agent to propose a bounded retry design, supplies system and rule versions, and grants read access. Editing code and accepting business risk remain outside its authority. The engineer retains ownership of open business questions.

The coding agent receives the approved design and applicable idempotency rule. It may edit scoped files and run listed tests. An unresolved shared-boundary question remains assigned to the engineer.

The human receives the diff, scope, rule, test results, and supporting impact analysis. Their duty is to verify implementation and assess the documented boundary finding. If accepting residual business risk requires a separate authority, the reviewer can escalate it.

[[L_EBG_A_07-3.png]]

This arrangement gives each receiver a usable basis and makes continuing responsibility explicit. It also creates an honest limit: a reviewer given only the diff can claim implementation review, while decision-risk review remains incomplete.

## Make the human checkpoint match the human duty

Oversight becomes meaningful when the person's task, information, access, and authority fit together. The same principle applies to agents continuing another agent's work.

Audit can compare the recorded transfer with those requirements. Governance then decides whether to continue, return, reroute, or correct the handoff.

Review your next approval checkpoint by asking what the recipient must judge and what in the received package lets them judge it. A mismatch identifies a handoff design problem that the workflow can address before responsibility reaches the receiver.

## Further Reading

- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)
- [Spark Tsai: Beyond HITL](https://doi.org/10.5281/zenodo.21856291)

#EngineeringBeforeGovernance #HumanOversight #AgentWorkflows #AIGovernance
