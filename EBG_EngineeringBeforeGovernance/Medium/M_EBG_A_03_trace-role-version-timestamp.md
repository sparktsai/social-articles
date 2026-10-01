# You Cannot Govern Evidence That Cannot Be Traced to One Engineering State

## A ticket, commit, or session ID can tell you where to look. It cannot tell you which role produced which engineering state, at what version, and at what time.

An AI agent is asked to change the retry behavior of a payment client.

The team has already captured Development Evidence. It knows which context fragments were sent, which alternatives appeared, which rule triggered, which option was selected, and what result was generated.

That is much better than a retrospective decision story.

Then an auditor tries to connect the evidence:

- Which exact decision used this context fragment?
- Was the rule evaluated by the system-design role or only cited later by a review role?
- Which version of the requirement, design, rule, test, or risk finding was involved?
- Did the decision occur before or after the architecture constraint changed?
- Does this evidence describe the same engineering state as the generated result?
- Which later correction replaced the original decision?

The evidence exists, but its engineering position is unclear.

That is the governance problem:

> If evidence cannot be bound to a fine-grained engineering object or behavior with a role, version, timestamp, and explicit relationships, governance can collect records but cannot reliably trace the state it is judging.

Before evidence can support repeatable governance, engineering must give each relevant state a stable coordinate.

---

## 1. Governance Problem: Evidence Without a Coordinate Becomes Another Search Problem

Article 02 separated Development Evidence from a polished explanation. It asked the engineering system to record what actually entered the generation, what actually appeared during the decision, what actually triggered, and what was actually produced.

But evidence still needs a place in the engineering structure.

Suppose a ticket contains one request, three generated designs, five code decisions, two rule triggers, a failed test, a reviewer correction, and a second generation. Giving all of them the ticket ID does not make them individually traceable. It only tells us that they happened somewhere inside the same container.

The same problem appears with a pull request, commit, conversation, or agent session. Each can contain many engineering states and many transitions between them.

```text
Ticket ID
    identifies a work container

Commit ID
    identifies a repository state

Session ID
    identifies an interaction container

Fine-grained Trace ID
    identifies one governable engineering unit and its relationships
```

The difference matters when a governance question becomes specific.

"Was the payment retry change reviewed?" can be answered at pull-request level.

"Did the system-design role apply `RULE-PAYMENT-IDEMPOTENCY@v4` to the decision that selected the retry strategy before the code was generated?" cannot.

That second question needs more than an ID. It needs the role under which the engineering state was formed, the exact versions involved, the time at which the state existed, and evidence that supports the claimed relationship.

Without those coordinates, governance falls back to searching logs, comparing timestamps by hand, reading conversations, and guessing whether two records refer to the same event.

Traceability then exists as a reconstruction exercise, not as an engineered property.

---

## 2. Existing Solutions Already Trace Important Things

Software engineering is not short of identifiers.

Issue trackers assign ticket IDs. Version-control systems identify commits and content states. Pull requests collect proposed changes and review. Requirements Traceability Matrices connect requirements to design, implementation, tests, and verification. Architecture Decision Records retain important decisions. Agent platforms and workflow engines assign run, task, conversation, and tool-call IDs.

Runtime observability offers an even more developed tracing model. W3C Trace Context defines a trace identifier for a distributed trace and a parent identifier for the current operation. OpenTelemetry represents individual operations as spans, with Trace IDs, Span IDs, parent relationships, links, attributes, events, and start and end timestamps.

These mechanisms solve real problems. They let operators follow a request across services, correlate logs, inspect an operation tree, or recover a repository state.

Provenance standards cover a different but related layer. W3C PROV models entities, activities, and agents. It can express usage, generation, derivation, attribution, association, revision, time, and the role an entity or agent played in an activity.

Put together, current practice gives us several useful capabilities:

```text
Work tracking identifies the delivery container
Version control identifies repository and content states
RTM connects declared lifecycle relationships
Distributed tracing follows runtime operations
Provenance models entities, activities, agents, roles, and derivation
```

The important point is not that these approaches are inadequate. They were designed for different questions.

A runtime Trace ID follows request execution. A commit hash identifies a source state. A ticket ID groups work. A provenance graph can describe rich relationships once the organization decides which entities and activities to capture.

What is still missing in many AI-assisted development workflows is a shared, fine-grained unit that connects one observable engineering state to its role, version, time, evidence, and related states.

---

## 3. What Existing Solutions Still Cannot Resolve

The first gap is granularity.

A single agent run may perform business analysis, propose system design, modify code, create tests, and write a summary. A run ID can connect those activities, but it cannot distinguish the individual engineering states that governance needs to compare.

The opposite problem also occurs. Raw telemetry may produce thousands of tool calls and token events. That data is detailed, but detail alone does not make it a useful governance unit. Governance usually needs to inspect a meaningful engineering object, behavior, or relationship, not every low-level event generated by the platform.

The second gap is role.

Knowing that `agent-session-8217` produced a statement does not tell us whether the statement represented business analysis, system design, architecture, implementation, verification, or review. The same human or AI actor can perform different functions during one workflow.

Role is therefore not the same as identity.

```text
Actor
    who or what performed the activity

Role
    the engineering function or viewpoint under which it acted
```

An AI agent may act as a system designer in one trace and as a developer in another. A human maintainer may review implementation evidence without being authorized to redefine a business requirement. Governance needs the role attached to the specific engineering activity, not merely a user name or model name.

The third gap is version.

A stable identifier such as `RULE-PAYMENT-IDEMPOTENCY` identifies a logical object. It does not tell us whether the decision used version 3 or version 4. A link to the latest document can silently change what an old trace appears to mean.

Version also has more than one layer:

- the version of the traced subject;
- the version of the Trace Record itself;
- the version of the trace schema used to interpret the record.

Mixing them makes later comparison unreliable.

The fourth gap is time.

One timestamp is often treated as enough, but "when it happened" and "when the system recorded it" are not always the same. OpenTelemetry's log model makes a similar distinction between an event timestamp and the time the collection system observed it.

For development governance, that difference matters. A rule may have changed between the decision and the later evidence capture. A trace reconstructed after review should not look as if it was captured during generation.

The final gap is coverage. Traceability is often designed around documents and code. But many governance-relevant units are neither:

- a delivered context fragment;
- an assumption;
- a generated alternative;
- a rule invocation;
- a decision;
- a tool action;
- a verification result;
- a risk finding;
- a correction;
- a handoff.

If the tracing model cannot identify these states, it cannot connect the behavior that occurred between the document and the code.

---

## 4. Governance Scope and the Traceability Engineering Elements

Let us narrow the scope before designing the record.

This article stays inside the software development stage. It does not attempt to replace runtime distributed tracing, organization-wide data lineage, or every identifier already used by engineering tools.

The governance unit is one engineering object, behavior, or relationship that can be independently inspected, compared, corrected, or handed off.

The specialized Governance Engineering Element introduced here is the **Traceability Engineering Element**:

```text
Traceable Engineering Unit
    = Trace ID
    + Subject
    + Role
    + Version
    + Timestamp
    + Relationships
    + Evidence
```

### Trace ID: Which unit are we talking about?

The Trace ID provides a stable identity for the unit. It should remain stable even when descriptive metadata is corrected.

The ID does not need to contain the role, version, and timestamp inside the string. Encoding every property into a long identifier makes the identifier brittle. Those properties belong in the Trace Record, where they can be queried and versioned without changing the identity of the trace.

### Subject: What is being traced?

The subject states what kind of engineering unit the trace represents.

It may be an entity, an activity, or a relationship. It may describe a requirement, context fragment, assumption, decision, rule invocation, code change, test result, risk finding, correction, or handoff.

This is what keeps the design from becoming document-centric or code-centric.

### Role: From which engineering function did it arise?

Role captures the function or viewpoint that gave the state its engineering meaning.

Examples include PM/BA business analysis, system design, system architecture, development, verification, security review, and governance audit.

The role should be separated from the actor:

```yaml
role:
  type: system-designer
  perspective: system-design

actor:
  type: ai-agent
  ref: agent-session-8217
```

This lets governance ask whether the necessary viewpoint was present without pretending that an actor has only one permanent role.

### Version: Which state existed at that point?

Version binds the trace to the state that actually existed. At minimum, distinguish the subject version from the Trace Record and schema versions.

```yaml
version:
  subject: v4
  trace_record: 1
  schema: "1.0"
```

For content-addressed artifacts, the subject version may be a Git object ID or integrity hash. For a rule, requirement, assumption, or decision, it may be a controlled version assigned by the relevant engineering system.

### Timestamp: When did it occur, and when was it observed?

The minimum useful distinction is:

```yaml
timestamp:
  occurred_at: 2026-09-30T10:24:18+08:00
  recorded_at: 2026-09-30T10:24:20+08:00
```

`occurred_at` identifies when the engineering event or state transition happened. `recorded_at` identifies when the trace infrastructure captured it.

If the original time is unavailable, say so. Do not replace an unknown occurrence time with the later recording time.

### Relationships: How does this unit connect?

A list of isolated IDs is not yet traceability. The Trace Record needs typed relationships such as:

```text
used
generated
derived_from
triggered
constrained_by
selected
rejected
modified
verified_by
superseded_by
handed_off_to
```

Typed relationships let Audit distinguish "the rule existed" from "the rule constrained this decision."

### Evidence: What supports the relationship?

Every important trace claim should point to the Development Evidence that supports it.

A relationship without evidence may still be a useful assertion, but it should not be presented as an observed fact.

This is the division of labor between Articles 02 and 03:

```text
Article 02: What observable decision behavior was captured?
Article 03: Where does each captured state belong, and how is it connected?
```

---

## 5. Engineering Fine-Grained Traceability

The engineering design begins at creation time.

Anchor Architecture describes an Anchor as a spatiotemporal coordinate that binds identity, location, and temporal state. That principle is useful here: a state that was not identifiable when created is difficult to recover later without speculation.

The Traceability Engineering Element adds the application-level meaning needed for development governance. It identifies the subject, role, version, timestamp, relationships, and supporting evidence around that coordinate.

### Capture the smallest meaningful unit

Do not assign one Trace ID to an entire project and call the work traceable. Also do not turn every token into a governance record.

Use the smallest unit that can be independently judged or changed.

For the payment retry example, these may be separate units:

```text
Context delivery
Retry-strategy decision
Idempotency-rule invocation
Generated implementation change
Verification result
Architecture-scope finding
```

They can share a parent change reference while retaining their own Trace IDs.

### Keep the ID stable and the record appendable

The ID should identify the trace, not describe its entire current state. Role, subject version, timestamps, and relationships belong in structured fields.

If a trace is corrected, retain the earlier record and append a new record version. Do not silently rewrite the past. If one engineering state replaces another, express `superseded_by` or another explicit relationship.

### Preserve both hierarchy and non-hierarchical links

Parent-child relationships are useful, but engineering work is not always a tree. One rule may constrain several decisions. One decision may affect several artifacts. One test may verify several changes.

The model therefore needs both:

```text
parent_trace_id
    structural containment or sequence

relations[]
    typed links across the wider engineering graph
```

This is one place where runtime tracing offers a useful lesson. OpenTelemetry uses parent relationships for nested work and links for causally related spans that do not fit one parent-child tree. Development traceability needs similar flexibility, but with engineering semantics rather than runtime request semantics.

### Separate captured facts from later claims

The trace infrastructure should preserve whether a relationship was observed, asserted, inferred, or verified.

```yaml
relation:
  type: constrained_by
  target: TRACE-RULE-IDEMPOTENCY-004
  basis: observed
  evidence: EVT-rule-trigger-021
  verification: pending
```

This prevents a later reviewer from turning a plausible connection into historical fact.

### Audit the trace, not only the traced result

Traceability itself can fail. Audit should be able to detect:

- duplicate or missing Trace IDs;
- unresolved subjects;
- role gaps;
- mutable references without versions;
- timestamps that violate the claimed order;
- relationships without evidence;
- incompatible schema versions;
- orphaned evidence;
- a generated result with no trace back to its decision basis.

Having Trace IDs does not mean the work has been governed. It means the organization has engineered units that can be followed and checked.

```text
Engineering creates traceable units
Evidence supports observed states and relationships
Audit checks trace integrity and claims
Governance judges and acts
```

That distinction keeps the PDCA loop concrete:

```text
Plan: define trace units, roles, version rules, time semantics, and required relationships
Do: assign traces as engineering states and behaviors occur
Check: audit identity, role, version, time order, relationships, and evidence coverage
Act: correct broken links, improve capture, or reject unsupported governance claims
```

---

## 6. Example: Tracing One Payment Retry Decision Beyond Documents and Code

Now return to the Development Evidence from Article 02.

The change is still associated with one parent development activity, but each governance-relevant state receives its own fine-grained Trace ID.

```yaml
development_trace:
  trace_id: TRACE-PAYMENT-RETRY-004
  parent_trace_id: TRACE-PAYMENT-RETRY-184

  subject:
    type: decision
    ref: DECISION-RETRY-STRATEGY-004
    description: Select retry behavior for temporary payment failures

  role:
    type: system-designer
    perspective: system-design

  actor:
    type: ai-agent
    ref: agent-session-8217

  version:
    subject: v1
    trace_record: 1
    schema: "1.0"

  timestamp:
    occurred_at: 2026-09-30T10:24:18+08:00
    recorded_at: 2026-09-30T10:24:20+08:00

  evidence_refs:
    - DEV-EVIDENCE-042
    - EVT-decision-023

  relations:
    - type: used
      target_trace_id: TRACE-CONTEXT-RETRY-003
      evidence: EVT-context-102

    - type: constrained_by
      target_trace_id: TRACE-RULE-IDEMPOTENCY-004
      evidence: EVT-rule-trigger-021

    - type: generated
      target_trace_id: TRACE-CHANGE-PAYMENT-CLIENT-006
      evidence: EVT-code-generation-026

    - type: verified_by
      target_trace_id: TRACE-TEST-PAYMENT-RETRY-007
      evidence: EVT-test-result-031
```

The related traces do not all point to documents or code.

`TRACE-CONTEXT-RETRY-003` identifies the delivered context state. `TRACE-RULE-IDEMPOTENCY-004` identifies a rule invocation. `TRACE-PAYMENT-RETRY-004` identifies the decision. `TRACE-CHANGE-PAYMENT-CLIENT-006` identifies the generated implementation state. `TRACE-TEST-PAYMENT-RETRY-007` identifies a verification result.

Each trace can carry its own role, actor, subject version, record version, schema version, occurrence time, recording time, relationships, and evidence.

That makes several audits possible without pretending to know the model's hidden reasoning:

```text
Role audit
    Was the decision formed under the required system-design viewpoint?

Version audit
    Did it use the rule and context versions valid at that time?

Temporal audit
    Did the rule invocation occur before the generated change?

Relationship audit
    Is the claim that the rule constrained the decision supported by evidence?

Continuity audit
    Can the later verification and correction be followed from the original decision?
```

The Trace ID does not decide whether the retry strategy is acceptable. Role does not grant authority by itself. Version does not prove correctness. Timestamp does not prove causality. Evidence does not make every relationship true.

Together, however, they create a small, inspectable engineering unit upon which Audit can operate and governance can make a supportable judgment.

> Evidence makes behavior observable. Fine-grained traceability gives that behavior an engineering coordinate. Governance still begins only when those coordinates and evidence are evaluated and acted upon.

---

## References

- [W3C Trace Context](https://www.w3.org/TR/trace-context/)
- [OpenTelemetry Tracing API](https://opentelemetry.io/docs/specs/otel/trace/api/)
- [OpenTelemetry Logs Data Model](https://opentelemetry.io/docs/specs/otel/logs/data-model/)
- [W3C PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/)
- [Git Internals: Git Objects](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects)
- [Decision Provenance: Harnessing Data Flow for Accountable Systems](https://www.repository.cam.ac.uk/items/14c68264-4c52-41d9-bf37-1dccc966cdcb)

### Related Work by the Author

- [Spark Tsai, *Anchor Architecture: A Minimal Structural Foundation for Software Traceability in AI-Assisted Software Development*](https://doi.org/10.31224/6580)
- [Spark Tsai, *Ghost Intent: An Effect of Traceability Collapse in GenAI-Assisted SDLCs*](https://doi.org/10.5281/zenodo.18872540)
- [Spark Tsai, *Viewpoint-Structured Specification (VSS)*](https://doi.org/10.31224/6612)
- [Spark Tsai, *Toward Decision Behavior Governance: Governance Existence, Invocation, and Decision Formation*](https://doi.org/10.5281/zenodo.18876165)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
