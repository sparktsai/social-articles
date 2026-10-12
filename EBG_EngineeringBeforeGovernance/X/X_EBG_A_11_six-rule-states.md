# “The AI Followed the Rule” Hides Six Different States

**Engineering Before Governance — Problem Deep Dive 03 / 04**

[[X_EBG_A_11-0.png]]

A team stores an idempotency rule in its repository. The rule appears in the agent’s final explanation. The generated payment code passes its tests.

Someone marks the change compliant.

That single label hides several different questions: Did the rule exist? Did it apply? Was it delivered? Did it visibly constrain a choice? Did the result satisfy it? Who judged the evidence?

Collapsing those questions into “followed” makes both engineering and governance less precise.

## State 1: Defined

A rule is **defined** when it has an identifiable meaning and version.

“Retries should be safe” expresses intent, but it is difficult to evaluate. A more operational rule is:

> Payment retry implementation MUST preserve the existing idempotency key for every retry attempt.

Definition should identify ownership and lifecycle state too. Without versioning, a reviewer cannot know whether today’s wording was the basis of yesterday’s decision.

## State 2: Applicable

A defined rule is **applicable** only when its conditions match the decision and scope.

The payment rule may apply to retry implementation but not to an unrelated logging change. Applicability is a judgment about the rule’s conditions, not evidence that the agent received or used it.

An effective ruleset should therefore bind exact versions to a bounded change rather than attach every organizational rule to every task.

## State 3: Invoked

A rule is **invoked** when evidence establishes that it entered the relevant decision basis.

A Context Manifest showing delivery of rule v4 before generation can support invocation. A rule file somewhere in the repository cannot. A final summary citing the rule afterward supports a declaration, not necessarily prior delivery.

This is where many “rule-following” claims lose their evidence connection.

## State 4: Influential

A rule is **influential** when observable evaluation shows how it constrained a candidate or selection.

For example, two generated retry options are recorded, and the new-key option is rejected under rule v4.

This supports a claim about visible decision behavior. It does not provide access to private reasoning or prove every internal influence. The boundary should remain explicit.

## State 5: Evaluated

A rule is **evaluated** when evidence supports satisfaction, violation, conflict, or uncertainty.

Review and tests may show that the final code reuses the existing key. That establishes artifact satisfaction under the tested conditions—even if invocation or influence was not captured.

The reverse is also possible: a rule can be delivered and visibly considered, while the resulting artifact still violates it.

## State 6: Governed

A rule is **governed** when an authorized role judges the finding and acts.

The action might be acceptance, correction, exception, escalation, or an improvement to the capture process. Evidence does not choose the action by itself; authority and policy still matter.

This state is why an automated compliance result is not the whole governance process.

## Report the states you can support

Suppose rule v4 was defined and selected as applicable. Delivery was not captured. The final summary cited it, and tests verified artifact satisfaction.

A precise report would say:

```text
Defined: supported
Applicable: supported
Invoked: unknown
Influential: unknown
Evaluated: satisfied under recorded tests
Governed: accepted with a capture-process finding
```

That record is more actionable than “compliant.” It shows that the artifact can be accepted while a process gap is still corrected.

Choose one rule in your current AI workflow. Which of the six states can your evidence actually support—and which are being inferred from the final result?

## Sources

- [RFC 2119: Requirement Levels](https://www.rfc-editor.org/info/rfc2119/)
- [Behavior Rule Architecture](https://doi.org/10.31224/6681)

#AIGovernance #BehaviorRules #AIEngineering #Compliance
