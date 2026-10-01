# Until Engineering Makes State Clear and Visible, Governance Cannot Judge

## Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State

[[M_EBG_A_01-0.png]]

In the final months of 2025, AI governance was being discussed across organizations, enterprises, governments, and technical communities. Organizations looked to standards such as ISO/IEC 42001 and AI management systems. Enterprises developed policies and SOPs. The topics ranged across responsible AI, data governance, ethics, security, runtime controls, and the growing use of agents in business and software development.

Across these different approaches, several familiar governance directions kept appearing: policy enforcement, authorization, human oversight, accountability, and audit. They tell an organization what it expects AI use to respect.

In October 2025, as I followed these discussions, I began asking a more specific question: how do these AI governance expectations become actionable inside software development? When I tried to apply them to engineering work, I found a large distance between the policy and the state an engineer could actually build, preserve, and show.

---

## 1. Governance Problem: Policy Does Not Tell an Engineer What to Build

“Enforce the policy.” “Use least-privilege authorization.” “Keep a human in the loop.” “Make someone accountable.” “Ensure the system is auditable.”

These are meaningful governance expectations. But presented to a software engineer as policies alone, they leave practical questions unanswered. What policy applied to this development decision? What did the AI agent actually receive? What was it authorized to change? What should the human review? Which evidence will later support an audit?

The gap is not that management or audit has failed to describe what it wants. The gap is that the expectation has not yet been translated into a development object, an engineering state, and a record that can support a judgment.

An organization may have an AI policy, an SOP, an approval workflow, and an audit requirement, while an individual AI-assisted change still leaves no clear record of its decision basis, applicable Rule, effective Scope, or handoff. The policy exists; the work continues; but the connection between them is missing.

---

## 2. Existing AI Governance Approaches Set Important Directions

AI governance already has substantial organizational and technical approaches. Standards such as [ISO/IEC 42001](https://www.iso.org/standard/42001) describe requirements for establishing and continually improving an AI management system. The [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) organizes AI risk work through Govern, Map, Measure, and Manage. Enterprise policies and SOPs assign responsibilities and define review and escalation processes. Security approaches such as identity management and Zero Trust constrain who or what can access systems. CI/CD pipelines can run checks and preserve development evidence.

Together, these approaches commonly lead to five governance directions:

**Policy enforcement** asks whether required or prohibited behavior can be applied to the system and its actions.

**Authorization** asks which actor may perform which action, on what object, and under what conditions.

**Human oversight** asks where human judgment is required and what decisions must be reviewed or escalated.

**Accountability** asks who is responsible for an action, decision, approval, or unresolved issue.

**Audit** asks whether the organization can inspect what happened and support its conclusions with evidence.

These policy directions are important. They help management establish expectations and organize controls. But when a team applies them to one AI-assisted development change, they still need an engineering answer: what state must be created so each expectation can be checked against the actual work?

[[M_EBG_A_01-1.png]]

---

## 3. Why Policy and Engineering Fail to Meet

When I tried to carry AI governance expectations into software development, two dependencies stopped the work from proceeding.

### Visibility Dependency

A governance judgment needs an identifiable object and state to inspect. If the team cannot tell which Scope or Rule applied, what context the agent received, or which version of an artifact was reviewed, management and audit cannot reliably judge the development action. They are left to infer or reconstruct it after the fact.

This is not a demand to expose every internal model operation. The question is whether the information needed for a specific governance judgment is visible to the responsible person or process.

### Operationalization Dependency

A governance requirement does not implement itself. Between “the agent must follow the Rule” and an enforceable, auditable development process, someone must determine how that Rule is identified, where its applicability is defined, whether it reaches the agent, what behavior can be observed, and what evidence should be retained.

The dependency is therefore more than a policy-to-tool mapping. It is a path from requirement, through engineering design and explicit state, to a governance mechanism that can evaluate and act. Without this path, the requirement remains valid, but its use in a particular development decision is difficult to establish.

[[M_EBG_A_01-2.png]]

---

## 4. Scope: Engineering Decision Behavior Governance

The question I began to study is bounded: how should AI-assisted software development decisions be governed while work is being developed, generated, reviewed, and handed off? This is not an attempt to cover every form of AI governance, every production-time runtime control, or every organizational policy.

The governance subject is **Engineering Decision Behavior**: observable decision-related behavior that occurs as AI participates in software development. The governance goal is not to reproduce private model reasoning. It is to identify the engineering elements needed to judge what happened, what basis applied, what changed, and whether the work may continue.

I use **Engineering Decision Behavior Framework (EDBF)** for the engineering foundation that organizes those elements. EDBF provides the basis for **Engineering Decision Behavior Governance**: applying governance requirements to development decision behavior through identifiable state, evidence, and reviewable relationships.

At a high level, the framework needs to make several kinds of engineering state connectable:

- the decision behavior and the Evidence captured around it;
- the identity and relevant state of each element, including role, version, or timestamp when needed;
- the Prompt, Context, system views, and change Scope that informed the work;
- applicable Rules and decision risks;
- the handoffs through which evidence, authority, and responsibility continue to another actor.

These policy directions are not yet engineering-element definitions. EDBF organizes the engineering elements that let policies about enforcement, authorization, oversight, accountability, and audit reach a specific development decision. The framework is the foundation; Engineering Decision Behavior Governance (EDBG) determines how the resulting state and Evidence are evaluated and what action follows.

---

## 5. Engineering Design: From Requirement to Evidence

The practical method begins with a governance requirement, but it does not stop at writing that requirement into an SOP. It proceeds through engineering work:

```text
Governance requirement
    What must management or audit be able to judge?

Current-state analysis
    What does the development process already capture?
    What is missing, transient, or disconnected?

Governance elements
    What objects and relationships are needed for the judgment?

Element externalization
    How will implicit context, scope, rules, roles, and decisions become explicit?

Engineering design
    Where and when are elements captured, identified, versioned, and linked?

Evidence
    What records show what happened and support a later judgment?

Audit design
    What will management or audit inspect, and what decision follows?
```

This order does not mean management waits until engineering is finished before defining governance. Management and auditors establish the requirement and the question to be answered at the outset. Engineering analysis then reveals what the current process can actually make visible and what elements or instrumentation are missing. With that engineering basis in place, management and audit can design a concrete inspection that is repeatable, proportionate, and grounded in available Evidence.

[[M_EBG_A_01-3.png]]

This also clarifies the meaning of “engineering before governance.” Governance requirements can guide engineering from the beginning. But a specific governance judgment can only be carried out once engineering has represented and preserved the relevant state.

---

## 6. A Governance Process That Can Be Repeated

Suppose an organization requires AI-generated software changes to follow approved Rules, remain within authorized Scope, and receive meaningful human review.

The engineering team first examines how a change currently moves through prompts, repositories, agents, tests, and review. It identifies what is already recorded and what disappears: perhaps the effective Context, the Rule version used, the decision basis, or the precise duty assigned to the reviewer. It then identifies those items as governance elements, designs how to represent and connect them, and produces Evidence from the development process.

Management and audit can now specify what they will inspect: whether the applicable Rule and Scope were present, whether the human received Evidence suitable for the assigned review, who owned any unresolved risk, and whether the record supports continuation. The audit criteria are no longer detached from the engineering process; they are built around state the process can actually produce.

Then the cycle continues:

```text
Plan: define the governance requirement and judgment
Do: analyze current practice and engineer the required elements
Check: evaluate the resulting Evidence against the requirement
Act: authorize, correct, return, escalate, and improve the design
```

This is the work of Engineering Decision Behavior Governance (EDBG), with EDBF as its engineering foundation. The purpose of this series is to show the process: what in software development needs governance, what engineering elements already exist or are missing, how to make them explicit, and how to design them into repeatable practice.

Without engineering elements and Evidence, AI governance remains too far from the development work it is meant to judge. With them, management and audit can move from broad policy to a specific, supportable decision.

---

## References

- [ISO/IEC 42001:2023, AI management systems](https://www.iso.org/standard/42001)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [NIST Secure Software Development Framework](https://csrc.nist.gov/projects/ssdf)
- [NIST DevSecOps Practices](https://pages.nist.gov/nccoe-devsecops/)
