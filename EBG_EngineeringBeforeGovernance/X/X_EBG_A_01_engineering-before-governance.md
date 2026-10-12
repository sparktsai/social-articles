# Your AI Policy Is Approved. What Should an Engineer Build Next?

**Engineering Before Governance — Main Series 01 / 08**

[[X_EBG_A_01-0.png]]

Your organization requires AI-generated changes to follow approved rules, stay within authorized scope, and receive human review.

An engineer opens a payment-service pull request. The tests pass. A reviewer approves it.

Can you show which rules the agent received, what it was allowed to change, and what the reviewer actually judged?

If answering requires someone to reconstruct a conversation, the policy has reached the approval workflow without reaching the engineering process beneath it.

## Policy needs an engineering subject

Requirements such as policy enforcement, authorization, oversight, and audit are meaningful. But each needs something observable against which it can be judged.

“Keep a human in the loop” leaves a practical question: what should that human inspect?

“Use least privilege” requires a boundary: which actions, on which artifacts, under which conditions?

“Make the change auditable” requires retained state: what happened, which version applied, and what supports the conclusion?

Policies and SOPs establish expectations. Git, tests, and review preserve useful parts of the work. The missing layer connects those pieces to one identifiable development decision.

For an AI-assisted payment retry change, that connection could include the approved scope, exact rule versions, context actually delivered, generated effect, verification, and evidence available to the reviewer.

## Design for visibility and operation

Two dependencies matter.

The first is **visibility**. A governance judgment needs a subject and historical state someone can inspect. A link to today’s specification cannot establish which version informed yesterday’s decision.

The second is **operationalization**. Someone must translate a requirement into capture and review mechanisms. Where is scope approved? How is context delivery recorded? What happens when evidence is insufficient?

Neither requires access to private model reasoning. Both require the external conditions and observable behavior relevant to the judgment.

## Start with one judgment

Consider this requirement:

> The agent must stay within the approved payment retry scope.

A workable engineering design would preserve:

- a versioned scope identifying permitted changes and exclusions;
- the request and context delivered to the agent;
- the generated artifact and its difference from the prior state;
- an analysis comparing the generated effect with the boundary;
- the finding, responsible authority, and resulting action.

A file diff might identify an unexpected edit. A structural review may still be needed if the change affects an interface or transaction boundary without expanding the file list.

The record enables the comparison. The authorized reviewer decides whether to accept, return, or make an exception.

## Build a repeatable path

The method is straightforward:

1. Define what management or audit must be able to judge.
2. Inspect what development already captures.
3. Identify missing objects, states, and relationships.
4. Make them explicit in the workflow.
5. Capture evidence as work occurs.
6. Compare it with the requirement and record the action.

I call the engineering foundation the **Engineering Decision Behavior Framework (EDBF)**. It organizes observable decision behavior and related engineering elements. **Engineering Decision Behavior Governance (EDBG)** uses that foundation to evaluate work and determine what follows.

The distinction matters. A framework represents state. Evidence supports a claim. Audit produces findings. Governance requires an authorized judgment and action.

Engineering before governance does not mean governance comes later. Governance requirements guide the work from the start. It means engineering must represent and preserve the relevant state before a specific governance judgment can be supported.

Choose one policy requirement and one AI-assisted change. What records would let another person judge it without relying on the original engineer’s memory?

## Sources

- [ISO/IEC 42001: AI management systems](https://www.iso.org/standard/42001)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [NIST Secure Software Development Framework](https://csrc.nist.gov/projects/ssdf)

#EngineeringBeforeGovernance #AIGovernance #SoftwareEngineering #AIEngineering
