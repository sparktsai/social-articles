# A Run ID Tells You Where the AI Worked—not Which Decision You Approved

**Engineering Before Governance — Problem Deep Dive 02 / 04**

[[X_EBG_A_10-0.png]]

An AI-assisted development run has one identifier. Inside it, the agent interprets a requirement, chooses a retry strategy, changes an interface, applies two rules, generates code, and revises the result after review.

The team approves the run.

Later, an auditor asks which decision was constrained by idempotency rule version 4.

The Run ID locates the container. It does not necessarily identify the decision inside it.

## Containers and decisions answer different questions

A Run ID is useful for questions such as:

- Which execution produced these logs?
- Which tools were available?
- When did the workflow start and end?
- Which outputs belong to the same operation?

A Decision ID supports a different set:

- Which bounded choice was made?
- What alternatives were visible for that choice?
- Which rule version applied?
- Which artifact did the choice generate?
- Was this decision later corrected or superseded?

Using a Run ID for both levels seems convenient until one run contains several choices with different evidence and consequences.

## One approval rarely means one judgment

Imagine a payment-service run with these decisions:

```text
D-101: classify the failure as retryable
D-102: reuse the existing idempotency key
D-103: limit retries to one attempt
D-104: keep the public API unchanged
D-105: modify a shared transaction helper
```

The run passes focused tests. A reviewer approves the pull request.

That approval may support a container-level statement: the pull request received review. It does not automatically show that the reviewer separately judged the authorization or evidence behind D-105.

If all five choices inherit the same undifferentiated status, the system cannot express that D-102 was verified, D-104 was explicitly approved, and D-105 remained outside scope.

## Give identity to what can change independently

Create a separate identity when an element must be independently inspected, related, corrected, or handed off.

A decision record does not need to contain an essay. It needs enough structure to connect:

- the parent run or development change;
- the bounded question and observable selection;
- applicable rule and context versions;
- generated or affected artifacts;
- verification and review findings;
- later correction or supersession.

The relationships matter as much as the fields:

```text
Run R-20 -> contains -> Decision D-105
Decision D-105 -> generated -> Artifact A-33
Decision D-105 -> evaluated_against -> Scope S-7
Finding F-9 -> identifies -> Out-of-scope effect
Decision D-106 -> supersedes -> Decision D-105
```

Now the correction does not rewrite the earlier history. It creates a new decision and a traceable relationship.

## Do not create IDs without resolution

More identifiers do not automatically create traceability.

An ID is useful only if it resolves consistently to the relevant record and historical state. A list of opaque IDs without typed relationships produces administrative noise.

Granularity also has a cost. Not every token, tool call, or intermediate sentence deserves independent governance identity. Use the smallest unit someone must judge or change separately.

If two choices always share the same basis, authority, artifact, and correction lifecycle, one bounded decision may be enough. If they can diverge, a shared Run ID is probably too coarse.

The threshold should also reflect consequence and reversibility. A low-impact formatting choice may remain inside the run record. A choice that changes authorization, interfaces, financial behavior, security posture, or acceptance evidence usually deserves an identity a reviewer can resolve independently. The goal is not maximum instrumentation. It is enough resolution for the judgments the organization genuinely needs to make.

Pick one AI-assisted run from your workflow. List the decisions that could be accepted, rejected, or corrected independently. Can your current identifier distinguish them without reopening the original conversation?

## Sources

- [W3C PROV-O](https://www.w3.org/TR/prov-o/)
- [W3C Trace Context](https://www.w3.org/TR/trace-context/)

#Traceability #AIGovernance #AIEngineering #SoftwareEngineering
