# The AI Explained Its Decision. What Can You Actually Verify?

**Engineering Before Governance — Main Series 02 / 08**

[[X_EBG_A_02-0.png]]

An AI agent says it compared three retry strategies, applied the payment idempotency rule, and selected the safest option.

The explanation is clear. The code looks reasonable.

Then a reviewer asks: were those alternatives recorded during generation, or written afterward for the summary?

That question changes what the record can support. A persuasive explanation can clarify a choice. By itself, it cannot establish what happened when the choice was made.

## A polished document can overstate the evidence

Tickets preserve requests. Specifications preserve intent. Commits preserve changes. Tool logs record selected actions. Approvals record acceptance.

Each answers a different question. Combining them into one decision document does not automatically establish the sequence or basis of a specific decision.

Suppose the summary cites `RULE-PAYMENT-IDEMPOTENCY@v4`. That establishes that the rule was cited. It does not establish whether the rule was delivered before selection, appeared in candidate evaluation, or was added afterward.

A required “alternatives considered” field can create the same problem. If generation moved directly to one option, inventing rejected alternatives makes the record less faithful, not more complete.

## Capture five observable parts

For a bounded engineering decision, preserve what can actually be observed:

1. **Context supplied.** Record the versioned sections or chunks delivered to the model. A specification in the repository is not the same as the fragments placed in context.
2. **Alternatives that appeared.** Retain candidates when they are visible in output or workflow events. If none appeared, leave that fact visible.
3. **Rules that visibly triggered.** Record the check or declared application, its version, and its recorded effect. A generated statement and an automated check are different evidence types.
4. **The decision that formed.** Give the bounded choice a stable Decision ID and preserve the observable selection event.
5. **The generated result.** Link the decision to the exact code or document so a reviewer can verify whether the output reflects the recorded choice.

These records describe external behavior. They do not expose or prove every internal influence on a model’s answer.

## Separate behavior, evidence, and claims

Imagine a payment retry record containing these events:

- the request and idempotency rule version 4 were delivered;
- generated candidates used either a new key or the existing key;
- a recorded evaluation rejected the new-key candidate;
- the selected option reused the existing key for one bounded retry;
- the generated code and test result were linked to that decision.

This supports a more precise conclusion than “the agent followed our rules.” A reviewer can inspect delivery, visible evaluation, selection, and artifact verification separately.

If the evaluation event is missing, preserve that limitation. Delivery may be established while participation in selection remains unknown. Passing tests may establish artifact compliance without resolving that uncertainty.

For every claim, ask: **which retained event supports it, and what does that event actually show?**

## Capture during the work

Assign identifiers at capture time. Bind inputs and outputs to exact versions. Link each decision to its parent change. Preserve observed events, then append corrections instead of rewriting history.

Do not record everything indiscriminately. Capture what the intended judgment requires, protect sensitive content, and keep references resolvable for authorized reviewers.

Evidence provides a basis for inspection. Audit evaluates the claims it can support. An authorized role accepts, corrects, returns, or escalates the work.

When a record is incomplete, the limitation is itself useful. It may justify additional verification, a new generation, or an improvement to the capture process.

Take one sentence in your next AI decision summary that says a rule shaped the choice. Can you follow it back to a recorded event, or only to another explanation?

## Sources

- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [Using Architectural Decision Records](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/introduction.html)
- [Toward Decision Behavior Governance](https://doi.org/10.5281/zenodo.18876165)

#EngineeringBeforeGovernance #AIGovernance #DecisionEvidence #SoftwareEngineering
