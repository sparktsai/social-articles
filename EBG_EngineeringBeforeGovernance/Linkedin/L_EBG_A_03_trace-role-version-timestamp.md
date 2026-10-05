# One Ticket, Five AI Decisions: Which One Did You Approve?

**Engineering Before Governance | 03 / 08**

If one AI-assisted ticket contains three designs, five code decisions, two rule checks, and a reviewer correction, how would you trace the rule that constrained one particular choice?

The ticket ID takes you to the work. The commit hash takes you to the code.

You still need a way to identify the decision, resolve the relevant rule version, and follow the evidence to the generated result.

That is where traceability becomes an engineering design problem.

[[L_EBG_A_03-0.png]]

## A container ID cannot answer every governance question

"Was this pull request reviewed?" is a container-level question.

"Did the system-design activity apply version 4 of the idempotency rule before selecting the retry strategy?" asks about individual elements and their relationships.

Both questions are legitimate. They need different records.

Issue trackers, Git, Requirements Traceability Matrices (RTMs), runtime tracing, and provenance models already identify useful things. A ticket groups delivery work. A commit identifies repository state. An RTM connects declared lifecycle relationships. A runtime trace connects execution operations.

Development governance needs those identifiers to connect to meaningful engineering units: context delivery, a decision, a rule invocation, an artifact, a test result, or a correction.

## Give each governed element an identity

[[L_EBG_A_03-1.png]]

A **Traceability Engineering Element** combines a stable identity, the relevant state, and explicit relationships to other identified elements. Evidence supports relationships when they make claims about what occurred.

Use the smallest unit that someone needs to inspect, compare, correct, or hand off independently.

For a payment retry change, the requirement, retry-strategy decision, idempotency-rule invocation, generated implementation, and verification result may each need separate identities. They can share a parent change reference.

An existing RTM ID, operation ID, or Decision ID can serve as the element's traceable identifier if it resolves uniquely and consistently. Otherwise, assign an identifier and retain the mapping to the native system.

This series uses "Trace ID" for that element-level identity. Keep its meaning explicit when integrating with runtime systems, where a Trace ID commonly identifies a distributed trace.

## Keep identity separate from changing state

The identifier answers "which element?" State answers "what was true of it at the relevant point?"

Record attributes according to the governance question:

- a requirement may need version and approval status;
- a decision activity may need role and event time;
- an artifact may need a commit or content hash;
- a correction may need a supersession link;
- an evidence record may need both event time and capture time.

Role, version, and timestamp are conditional. Requiring every field on every element adds noise and can encourage fabricated precision.

Keep actor and role distinct. The same agent can perform analysis and implementation in one workflow. The role describes the function of the activity; it does not grant authority automatically.

[[L_EBG_A_03-3.png]]

## Make each relationship say what it means

A list of IDs is difficult to interpret. Typed relationships let a reviewer follow the chain:

```text
Requirement -> assigned_to -> Development operation
Operation -> contains -> Retry decision
Decision -> constrained_by -> Idempotency rule v4
Decision -> generated -> Payment client at a specific commit
Artifact -> verified_by -> Retry test result
```

Where the chain asserts that a rule constrained a choice, link the supporting event. Where an RTM declares that a test verifies a requirement, preserve that declared relationship without presenting it as proof that the test ran during this change.

Relationships may be observed, asserted, inferred, or verified. Keeping that basis visible prevents a plausible connection from becoming a historical fact by repetition.

Engineering work also forms a graph. One rule can constrain several decisions; one test can cover several artifacts. Preserve cross-links as well as parent-child structure.

[[L_EBG_A_03-2.png]]

## Audit the chain as well as the code

A useful trace review checks whether identifiers resolve, historical versions remain recoverable, required state is present, and claimed relationships have support.

A timestamp can help check an alleged sequence. It cannot establish causality on its own. A role can explain a viewpoint. It cannot establish authorization. A version identifies state. It cannot prove correctness.

Keep corrections appendable. When a later decision supersedes the original, retain both and connect them explicitly. A link to the latest document should never silently redefine the basis of an old decision.

The practical test is simple: pick one approved AI-generated change and follow it back through its decision, context, applicable rule, and verification. Every unresolved link identifies a concrete improvement to the tracing design.

## Further Reading

- [W3C PROV-O](https://www.w3.org/TR/prov-o/)
- [W3C Trace Context](https://www.w3.org/TR/trace-context/)
- [Spark Tsai: Anchor Architecture](https://doi.org/10.31224/6580)

#EngineeringBeforeGovernance #Traceability #AIGovernance #SoftwareEngineering
