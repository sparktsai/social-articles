# Your AI Policy Requires Oversight. How Will You Know It Improved?

**Engineering Before Governance — Main Series 08 / 08**

[[X_EBG_A_08-0.png]]

Your organization requires AI-generated changes to follow rules, respect authorization, and receive human oversight.

After a failure, it updates the policy and adds another approval.

How would you show that the process actually improved?

The team needs a connection between the original finding, the engineering change made in response, and evidence from later work. Without that connection, a correction may be visible while improvement remains an assumption.

## Begin with one judgment

This series focuses on observable decision behavior in AI-assisted software development: what a change was based on, which boundaries applied, what it affected, and whether people could perform their assigned responsibilities.

Governance requirements establish the questions. Engineering analysis identifies the objects, states, and relationships that must be captured. Evidence and traceability give an authorized reviewer material for a supportable judgment.

The **Engineering Decision Behavior Framework (EDBF)** represents those elements. **Engineering Decision Behavior Governance (EDBG)** uses that foundation to evaluate requirements, assign responsibility, and act.

The distinction keeps the claim precise. Capturing a record supplies infrastructure. Governance occurs when a responsible authority uses it to decide what follows.

## Evidence and traceability create the foundation

Development Evidence preserves the context actually supplied, alternatives when visible, observable rule triggers, the decision, and its generated result. It keeps capture limits explicit instead of inventing missing events.

Traceability gives relevant elements identities, historical state, and typed relationships. A requirement, decision, artifact, test, correction, and handoff can be followed without assuming one ticket ID identifies them all.

Those foundations support four practical applications:

- compare expected context with what was delivered;
- distinguish rule definition, application evidence, and artifact satisfaction;
- connect decision conditions to impact, controls, and residual uncertainty;
- establish what each receiver obtained and who owns unresolved work.

Together, they let a review inspect development conditions instead of looking only at final code.

## A correction is not yet an improved process

Suppose an audit of a payment retry change finds two problems: required architecture delivery cannot be established, and the diff exceeds approved scope.

The organization returns the change. Engineering adds context capture and a scope comparison. A new generation receives the approved architecture viewpoint and removes the unsupported modification.

The resulting evidence supports treatment of those conditions. The original record keeps its limitation and links to the corrected decision.

That is a useful correction. To establish improvement, inspect later payment changes too. Was required context consistently captured? Did scope checks detect unexpected effects? Could reviewers resolve references and perform their duties?

Those observations distinguish a reliable practice from a one-time repair.

## Make PDCA observable

**Plan:** choose a bounded governance requirement, expected state, decision authority, and required evidence.

**Do:** perform development under that basis. Capture delivery, observable decisions, generated effects, checks, and handoffs as they occur.

**Check:** compare expected basis and result with retained evidence. Separate supported findings from unknowns. Check whether the reviewer had enough information for the assigned judgment.

**Act:** correct the result or improve context design, rules, tracing, controls, permissions, or handoffs. Retain the action and examine its effect in later work.

Each step has an identifiable subject and record. The next cycle can therefore learn from the prior one.

These capabilities do not guarantee compliance. They give management and audit concrete places to inspect, intervene, and improve.

Begin with one consequential change and one policy requirement. Define the judgment, build the evidence connection, retain the response, and use the next change to test whether the response held.

Which control in your current AI workflow was added after a failure—and what later evidence shows that it improved the process?

## Sources

- [ISO/IEC 42001: AI management systems](https://www.iso.org/standard/42001)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

#EngineeringBeforeGovernance #AIGovernance #ContinuousImprovement #SoftwareEngineering
