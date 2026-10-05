# Your AI Policy Is Approved. What Should an Engineer Build Next?

**Engineering Before Governance | 01 / 08**

Your organization requires AI-generated changes to follow approved rules, stay within authorized scope, and receive human review.

An engineer opens a payment-service pull request. The tests pass. A reviewer approves it.

Can you show which rules the agent received, what it was authorized to change, and what the reviewer actually judged?

If those questions require someone to reconstruct a conversation, the policy has reached the approval process without reaching the engineering process that should support it.

[[L_EBG_A_01-0.png]]

## The missing step between policy and a development decision

Policy enforcement, authorization, human oversight, accountability, and audit are meaningful expectations. Each needs an engineering object against which it can be checked.

"Keep a human in the loop" leaves a practical question: what should that human inspect?

"Use least privilege" requires a boundary: which actions, on which artifacts, under which conditions?

"Make the change auditable" requires retained records: what happened, which state applied, and what supports the conclusion?

Policies, SOPs, and approval workflows establish expectations and responsibilities. Git, tests, and review preserve useful parts of the work. The remaining task is to connect those pieces to one identifiable development decision.

For an AI-assisted payment retry change, that connection might include the approved change boundary, the exact rule versions, the context actually delivered, the generated effect, and the evidence available to the reviewer.

## Two dependencies worth designing explicitly

[[L_EBG_A_01-1.png]]

The first is **visibility**. A governance judgment needs a subject and state that someone can inspect. A link to today's specification cannot establish which specification version informed yesterday's decision.

The second is **operationalization**. Someone must translate the requirement into a capture and review mechanism. Where is the rule selected? When is the scope approved? How is context delivery recorded? What happens when the evidence is insufficient?

Neither dependency requires access to private model reasoning. Both require the external conditions and observable behavior relevant to the judgment.

This series focuses on decision behavior during AI-assisted software development: requirements, design, generation, verification, and handoff. The question is how to make that work inspectable enough for a responsible authority to decide whether it may continue.

## Start with the judgment you need to make

[[L_EBG_A_01-2.png]]

Consider the requirement: "The agent must stay within the approved payment retry scope."

A workable engineering design would preserve:

- a versioned scope identifying permitted changes and exclusions;
- the request and context delivered to the agent;
- the generated artifact and its difference from the prior state;
- an analysis comparing the generated effect with the approved boundary;
- the finding, responsible authority, and resulting action.

A file-level comparison may identify an unexpected edit. A structural review may also be needed when a change affects an interface or transaction boundary without expanding the list of edited files.

The engineering record makes the comparison possible. The authorized reviewer decides whether to accept the change, return it, or approve an exception.

[[L_EBG_A_01-3.png]]

## A repeatable path from requirement to action

The method behind this series is straightforward:

1. Define what management or audit must be able to judge.
2. Inspect what the development process already captures.
3. Identify the missing objects, states, and relationships.
4. Make those elements explicit in the workflow.
5. Capture evidence as the work occurs.
6. Compare the evidence with the requirement and record the action.

I call the engineering foundation the **Engineering Decision Behavior Framework (EDBF)**. It organizes observable decision behavior and its related elements. **Engineering Decision Behavior Governance (EDBG)** uses that foundation to evaluate work and determine what follows.

The distinction matters. A framework can identify state. Evidence can support a claim. An audit can produce a finding. Governance requires an authorized judgment and action.

## What "engineering before governance" means in practice

Governance requirements guide the work from the beginning. Engineering must represent and preserve the relevant state before a specific governance judgment can be supported.

That creates a practical improvement loop: define the requirement, perform and capture the work, inspect the evidence, then correct the result or improve the capture mechanism.

The next time an AI policy reaches your engineering team, choose one requirement and one development change. Ask what records would let another person judge that requirement without relying on the original engineer's memory.

That is a concrete place to begin.

## Further Reading

- [ISO/IEC 42001: AI management systems](https://www.iso.org/standard/42001)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [NIST Secure Software Development Framework](https://csrc.nist.gov/projects/ssdf)
