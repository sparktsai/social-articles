# The AI Explained Its Decision. What Can You Actually Verify?

**Engineering Before Governance | 02 / 08**

An AI agent says it compared three retry strategies, applied the payment idempotency rule, and selected the safest option.

The explanation is clear. The code looks reasonable.

Then a reviewer asks: were those alternatives recorded during generation, or written afterward to complete the summary?

That question changes what the record can support. A persuasive explanation can help someone understand a choice. It cannot, by itself, establish what happened when the choice was made.

[[L_EBG_A_02-0.png]]

## Why a decision document can overstate the evidence

Tickets preserve requests. Specifications preserve intent. Commits preserve changes. Tool logs record selected actions. Approvals record acceptance.

Each artifact answers a different question. Combining them in a polished decision document does not automatically establish the sequence or basis of one decision.

Suppose the final summary cites `RULE-PAYMENT-IDEMPOTENCY@v4`. That shows the rule was cited. It leaves open whether the rule was delivered before selection, appeared in candidate evaluation, or was added to the explanation afterward.

Likewise, a required "alternatives considered" field can encourage retrospective completion. If the generation moved directly to one option, inventing a rejected alternative makes the record less faithful.

Architecture Decision Records are valuable for preserving a choice and its consequences. Provenance connects actors, activities, and artifacts. Telemetry captures selected events. The engineering task here is to connect those capabilities around a bounded decision event.

## Capture five observable parts of the decision

**The context actually supplied.** Record the versioned sections or chunks delivered to the model. A hundred-page specification in the repository is different from the three sections included in context.

**Alternatives that actually appeared.** Retain candidate options when they are observable in generated output or workflow events. When none appeared, leave that fact visible.

**Rules that visibly triggered.** Record an observable rule check or declared application, its version, and the recorded effect on a candidate. Keep the evidence type clear: a generated statement about using a rule has different strength from a recorded automated check.

**The decision that formed.** Give the bounded choice a stable Decision ID and retain the observable selection event.

**The generated result.** Connect the decision to the exact document or code artifact so a reviewer can check whether the output reflects the recorded choice.

These records describe external behavior. They do not establish every internal influence on a model's answer.

[[L_EBG_A_02-2.png]]

## Keep behavior, evidence, and claims separate

For the payment retry example, imagine the capture layer retains these events:

1. The request and idempotency rule version 4 were delivered.
2. Generated candidates included retrying with a new key and retrying with the existing key.
3. A recorded evaluation rejected the new-key candidate under the rule.
4. The selected option reused the existing key for one bounded retry.
5. The generated code and a test result were linked to that decision.

This supports a more specific claim than "the agent followed our rules." A reviewer can inspect the delivered basis, the visible candidate evaluation, and artifact verification separately.

If event 3 is missing, the record should preserve that limitation. Delivery may be established while participation in candidate evaluation remains unknown. Passing tests may establish artifact compliance without resolving that uncertainty.

The useful discipline is to ask of every claim: **which retained event supports it, and what does that event actually show?**

## Build the capture layer into generation

Assign identifiers at the point of capture. Bind inputs and outputs to exact versions. Link the decision to its parent change. Preserve observed events and append later corrections rather than rewriting history.

This is the role of the Evidence Skill that motivated the original article: preserve supplied context, observable alternatives, triggered rules, decisions, and generated results. Its value depends on faithful capture and clear limits.

Recording everything indiscriminately creates another search problem. Capture the information needed for the judgment, with controlled storage for sensitive material and resolvable references in the evidence record.

## What governance does with the record

Evidence provides a basis for inspection. Audit evaluates the claims it can support. An authorized role then accepts, corrects, returns, or escalates the work.

When the record is incomplete, that limitation is itself useful information. It may justify additional verification, a new generation, or an improvement to the capture process.

Before approving the next AI-generated decision summary, choose one sentence that claims a rule shaped the choice. Follow it back to the recorded event. The strength of that connection determines how much confidence the summary deserves.

## Further Reading

- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [Using Architectural Decision Records](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/introduction.html)
- [Spark Tsai: Toward Decision Behavior Governance](https://doi.org/10.5281/zenodo.18876165)
