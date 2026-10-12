# An AI Explanation Is Not Evidence of How the Decision Happened

**Engineering Before Governance — Problem Deep Dive 01 / 04**

[[X_EBG_A_09-0.png]]

An AI coding agent produces a clean decision summary:

> I considered three retry strategies, applied the idempotency rule, and chose the safest option.

The explanation is plausible. It may even describe the final code accurately.

But what exactly does it prove about the decision process?

Unless the alternatives, rule application, and selection were captured as observable events, the summary establishes what the model said afterward—not necessarily what happened before the code was generated.

## A useful explanation can still be weak evidence

Explanations help people understand, review, and challenge a result. The problem begins when readability is treated as provenance.

A generated summary can combine material from the prompt, final artifact, conversation history, and requested reporting format. It may reconstruct a coherent rationale even when the workflow retained no event showing that the stated comparison occurred.

This does not mean the explanation is false. It means the explanation and the historical claim are different objects.

“The final code preserves the idempotency key” can be checked against the artifact.

“The idempotency rule caused the agent to reject another candidate” requires evidence of a rule-linked evaluation before or during selection.

The first is a result claim. The second is a process claim.

## Four evidence types support different conclusions

Consider four records that might mention the same rule.

**1. Generated statement**

The agent says it followed the rule. This establishes a declared explanation. It can guide review, but it does not independently verify delivery, evaluation, or compliance.

**2. Context delivery record**

A manifest shows that rule version 4 was delivered before the decision. This supports availability in the decision basis. It does not prove that the rule affected selection.

**3. Observable evaluation event**

A workflow event links the rule to two visible candidates and records why one was rejected. This supports a claim about the rule’s recorded participation in the choice. It still does not reveal every internal model influence.

**4. Artifact verification**

A test and reviewer confirm that every retry reuses the original idempotency key. This supports satisfaction by the result. It does not retroactively prove how the result was selected.

These records are complementary. None should silently inherit the meaning of another.

## Preserve unknowns instead of completing the story

Suppose only the generated statement and passing test exist.

A defensible conclusion is:

> The agent declared that it applied rule v4, and the resulting artifact satisfies the tested condition. Whether that rule was delivered before selection or visibly evaluated against alternatives was not captured.

That language is less elegant than “the AI followed the rule,” but it is more useful. It tells a reviewer what is established, what remains unknown, and which capture mechanism would improve the next run.

Retrospectively adding alternatives or converting a summary into an event log makes the record look complete while weakening its integrity.

## Design the workflow around the claim

Before requesting a decision summary, decide which claim the organization needs to support.

If the goal is artifact acceptance, tests and review may be sufficient.

If the goal is policy enforcement during generation, capture exact rule delivery, observable evaluation, decision identity, and the connection to the resulting artifact.

If the platform cannot expose one of those events, record that limitation. Do not replace missing evidence with confident prose.

The practical test is simple: remove the AI-generated explanation from the record. What evidence remains for each sentence you planned to approve?

## Sources

- [W3C PROV Overview](https://www.w3.org/TR/prov-overview/)
- [Using Architectural Decision Records](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/introduction.html)

#AIGovernance #DecisionEvidence #AIEngineering #SoftwareEngineering
