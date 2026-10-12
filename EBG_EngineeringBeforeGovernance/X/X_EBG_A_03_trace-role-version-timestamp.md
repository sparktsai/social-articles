# One Ticket, Five AI Decisions: Which One Did You Approve?

**Engineering Before Governance — Main Series 03 / 08**

[[X_EBG_A_03-0.png]]

One AI-assisted ticket contains three designs, five code decisions, two rule checks, and a reviewer correction.

How would you trace the rule that constrained one particular choice?

The ticket ID takes you to the work. The commit hash takes you to the code. Neither necessarily identifies the decision, its rule version, or the evidence connecting it to the result.

That is where traceability becomes an engineering design problem.

## A container ID answers container questions

“Was this pull request reviewed?” is a container-level question.

“Did the design activity apply version 4 of the idempotency rule before selecting the retry strategy?” asks about individual elements and their relationships.

Both are legitimate. They need different records.

Issue trackers, Git, Requirements Traceability Matrices, runtime traces, and provenance models already identify useful things. A ticket groups delivery work. A commit identifies repository state. An RTM declares lifecycle relationships. A runtime trace connects execution operations.

Development governance must connect these identifiers to meaningful units such as context delivery, a decision, rule invocation, artifact, test result, or correction.

## Identify the smallest governed element

A **Traceability Engineering Element** combines a stable identity, relevant state, and explicit relationships to other identified elements. Evidence supports relationships when they make claims about what occurred.

Use the smallest unit someone needs to inspect, compare, correct, or hand off independently.

For a payment retry change, the requirement, retry-strategy decision, idempotency-rule invocation, generated implementation, and verification result may each need an identity. They can still share one parent change reference.

An existing RTM ID, operation ID, or Decision ID can serve as the identifier if it resolves uniquely and consistently. Otherwise, assign one and retain a mapping to the native system.

## Identity is not state

The identifier answers “which element?” State answers “what was true of it at the relevant point?”

Record attributes according to the judgment:

- a requirement may need version and approval status;
- a decision activity may need role and event time;
- an artifact may need a commit or content hash;
- a correction may need a supersession link;
- evidence may need event time and capture time.

Role, version, and timestamp are conditional. Requiring every field for every element adds noise and can encourage fabricated precision.

Keep actor and role distinct too. The same agent may perform analysis and implementation. The role describes the function of an activity; it does not automatically grant authority.

## Relationships need meaning

A list of IDs is not a trace. Typed relationships allow a reviewer to follow the chain:

```text
Requirement -> assigned_to -> Development operation
Operation -> contains -> Retry decision
Decision -> constrained_by -> Idempotency rule v4
Decision -> generated -> Payment client at commit X
Artifact -> verified_by -> Retry test result
```

Where the chain claims that a rule constrained a choice, link the supporting event. Where an RTM says a test verifies a requirement, keep that declared relationship without presenting it as proof that the test ran for this change.

Relationships may be observed, asserted, inferred, or verified. Showing that basis prevents a plausible connection from becoming a historical fact through repetition.

## Audit the chain, not just the code

A trace review should ask whether identifiers resolve, historical versions remain recoverable, required state is present, and claimed relationships have support.

A timestamp may support sequence; it does not establish causality. A role may explain a viewpoint; it does not establish authorization. A version identifies state; it does not prove correctness.

Corrections should be appendable. When a later decision supersedes the original, preserve both and connect them explicitly. A link to the latest document must not silently redefine the basis of an earlier decision.

Pick one approved AI-generated change and follow it through its decision, delivered context, applicable rule, artifact, and verification. Which link fails to resolve without asking the original engineer?

## Sources

- [W3C PROV-O](https://www.w3.org/TR/prov-o/)
- [W3C Trace Context](https://www.w3.org/TR/trace-context/)
- [Anchor Architecture](https://doi.org/10.31224/6580)

#EngineeringBeforeGovernance #Traceability #AIGovernance #SoftwareEngineering
