# A Human Approved the AI Change. Did They Have Enough to Judge It?

**Engineering Before Governance — Main Series 07 / 08**

[[X_EBG_A_07-0.png]]

“A human makes the final decision.”

That can provide valuable oversight. It can also assign someone a responsibility the handoff leaves them unable to perform.

A reviewer with a diff and passing tests can inspect implementation. If asked to approve architecture impact and residual business risk, they need additional analysis and authority.

The checkpoint is visible. The conditions for meaningful review may still be missing.

## Work can move while responsibility disappears

Consider a payment retry change moving from an engineer to an analysis agent, then a coding agent, and finally a human reviewer.

The first agent receives a vague request. The coding agent receives a short design summary. The reviewer receives the pull request.

Every transfer completes. Yet who owns the unresolved transaction-boundary question? Which constraints reached the coding agent? What exactly must the human judge?

Tickets, prompts, protocols, checkpoints, and pull requests support routing. A transfer event alone does not establish that the receiver has the information, access, authority, and capacity needed for the next task.

## Three directions need different packages

**Human to agent (H2A).** The agent needs the actual instruction, delivered context, expected outcome, approved scope, applicable rules, exclusions, and escalation conditions. A request for analysis should say whether editing code is authorized.

**Agent to agent (A2A).** The receiving agent needs the relevant payload, source references, assigned role, and a clear separation between established decisions and unresolved assumptions. Access to an analyst’s output does not grant authority to accept risk.

**Agent to human (A2H).** The human needs a specific duty and material that supports it. Code review needs the diff, requirements, scope, rules, and verification. Decision-risk review may also need alternatives, assumptions, impact analysis, controls, and residual risk.

In every direction, unresolved items need named owners. A conversation summary should not become the place where responsibility disappears.

## Capture what crossed the boundary

Give the handoff an identity and connect it to sending and receiving activities. Record the actual payload with versioned references to relevant decisions, artifacts, scope, rules, risk, and evidence.

Record filtering and summarization when observable. A full history can carry stale context; a short summary can omit a constraint. The right package depends on the receiver’s task.

Preserve the difference between prepared, sent, received, accessible, assessed, accepted, and returned. A sent reference may be inaccessible. Receipt establishes transfer; acceptance records a response. Neither proves that the next decision was sound.

Before work continues, compare the package with the responsibility. Can the receiver resolve the references? Is the permitted next action clear? Does every open issue have an owner? Can a human return or escalate insufficient work?

## Match the checkpoint to the duty

In a better payment workflow, the analysis agent receives system and rule versions plus read-only authority. Editing and risk acceptance remain outside its role.

The coding agent receives an approved design, applicable rule, scoped files, and listed tests. An unresolved shared-boundary question remains assigned to the engineer.

The human receives the diff, scope, rule, test results, and impact analysis. Their duty is to verify implementation and assess the documented boundary finding. Residual business risk is escalated if it requires different authority.

This arrangement creates an honest limit: a reviewer given only the diff can claim implementation review, while decision-risk review remains incomplete.

Oversight becomes meaningful when task, information, access, and authority fit together. Audit can compare the transfer with those requirements. Governance can then continue, return, reroute, or correct the work.

At your next approval checkpoint, what must the reviewer judge—and which item in the received package makes that judgment possible?

## Sources

- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)
- [Beyond HITL](https://doi.org/10.5281/zenodo.21856291)

#EngineeringBeforeGovernance #HumanOversight #AgentWorkflows #AIGovernance
