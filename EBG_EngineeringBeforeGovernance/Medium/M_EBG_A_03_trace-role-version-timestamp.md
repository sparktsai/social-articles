# You Cannot Govern What You Cannot Identify and Trace

## Give each element a traceable identity, then connect its changing state to the rest of the engineering chain.

[[M_EBG_A_03-0.png]]

An AI agent is asked to change the retry behavior of a payment client.

The team has already captured Development Evidence. It knows which context fragments were sent, which alternatives appeared, which rule triggered, which option was selected, and what result was generated.

That is much better than a retrospective decision story.

Then an auditor tries to connect the evidence to the engineering elements around it:

- Which exact decision used this context fragment?
- Was the rule evaluated by the system-design role or only cited later by a review role?
- Which version of the requirement, design, rule, test, or risk finding was involved?
- Did the decision occur before or after the architecture constraint changed?
- Does this evidence describe the same engineering state as the generated result?
- Which later correction replaced the original decision?

The evidence exists, but the elements it describes cannot be reliably identified and connected.

That is the governance problem:

> If governance-relevant elements do not have stable traceable identities, and their relevant changing states and relationships are not recorded, governance can collect evidence but cannot follow what it is judging across the development chain.

Before evidence can support repeatable governance, engineering must identify each element and preserve the states and links needed to follow it.

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

Traceability Identifier
    identifies a governance-relevant element

Trace chain
    connects identified elements through explicit relationships
```

The difference matters when a governance question becomes specific.

"Was the payment retry change reviewed?" can be answered at pull-request level.

"Did the system-design role apply `RULE-PAYMENT-IDEMPOTENCY@v4` to the decision that selected the retry strategy before the code was generated?" cannot.

That second question needs each relevant element to be identifiable, the role, version, or time state when relevant, and evidence for the claimed relationships. Role, version, and timestamp are not mandatory properties of every element. They are traceable engineering elements or state attributes when the governance question needs them.

Without those coordinates, governance falls back to searching logs, comparing timestamps by hand, reading conversations, and guessing whether two records refer to the same event.

Traceability then exists as a reconstruction exercise, not as an engineered property.

[[M_EBG_A_03-1.png]]

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

What is still missing in many AI-assisted development workflows is a consistent way to identify every element that needs governance and connect it to the other elements involved. RTM references, Operation IDs, Decision Execution IDs, rules, scope items, evidence, and artifacts should be linkable without assuming they are all the same kind of identifier.

---

## 3. What Existing Solutions Still Cannot Resolve

The first gap is granularity.

A single agent run may perform business analysis, propose system design, modify code, create tests, and write a summary. A run ID can connect those activities, but it cannot distinguish the individual engineering states that governance needs to compare.

The opposite problem also occurs. Raw telemetry may produce thousands of tool calls and token events. That data is detailed, but detail alone does not make it a useful governance unit. Governance usually needs to inspect a meaningful engineering object, behavior, or relationship, not every low-level event generated by the platform.

The second gap is role and other changing state.

Knowing that `agent-session-8217` produced a statement does not tell us whether the statement represented business analysis, system design, architecture, implementation, verification, or review. The same human or AI actor can perform different functions during one workflow.

Role is therefore not the same as identity. It is one possible state or perspective associated with an element or activity.

```text
Actor
    who or what performed the activity

Role
    the engineering function or viewpoint under which it acted
```

An AI agent may act as a system designer in one trace and as a developer in another. A human maintainer may review implementation evidence without being authorized to redefine a business requirement. When role matters to a governance question, record it against the specific activity. Other elements may instead need a version, timestamp, status, or location; choose state attributes according to the element and governance question.

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

The final gap is coverage. Traceability is often designed around documents and code. But many governance-relevant elements are neither:

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

The specialized Governance Engineering Element introduced here is the **Traceability Engineering Element**. Every element that must be governed receives a stable traceable identifier. A trace record then captures that element's relevant state and connects it to other identified elements.

```text
Traceability Engineering Element
    = Element Identity
    + Relevant Current State
    + Relationships to Other Identified Elements
    + Supporting Evidence, when needed
```

### Traceable Identity: Which element are we talking about?

Every element selected for governance receives a Trace ID: an identifier that lets other records refer to that specific element. An existing RTM ID, Operation ID, or Decision Execution ID can serve as its Trace ID when it uniquely and consistently identifies the element in the trace chain. If it does not, the traceability layer assigns its own ID and maps it to the native identifier. The identity stays stable while the element's state can change over time.

The identifier does not need to encode role, version, timestamp, or status in its string. Those values describe the element's state at a point in time. Record identity and state separately so each state change does not look like a different logical element.

### Subject: What is being traced?

The element states what is being governed and what type of thing it is.

It may be an entity, an activity, or a relationship. It may describe a requirement, context fragment, assumption, decision, rule invocation, code change, test result, risk finding, correction, or handoff.

This is what keeps the design from becoming document-centric or code-centric.

### State: What was true of this element at the time?

An element may have changing state that governance needs to inspect. Depending on the element, that can include:

- version of a requirement, rule, specification, artifact, or trace record;
- timestamp when a decision, operation, update, or observation occurred;
- role or viewpoint associated with an activity or representation;
- status such as proposed, active, superseded, verified, or unresolved;
- location, scope, authority, or lifecycle state.

These fields are conditional. A requirement may need a version and lifecycle status. A decision activity may need role and timestamp. A code artifact may need a commit or content hash. Record the state relevant to the governance question rather than requiring every possible field everywhere.

[[M_EBG_A_03-3.png]]

When role is recorded, separate it from the actor:

```yaml
role:
  type: system-designer
  perspective: system-design

actor:
  type: ai-agent
  ref: agent-session-8217
```

This lets governance ask whether the necessary viewpoint was present without pretending that an actor has only one permanent role. Role can also be modeled as its own identified element when its definition or version needs independent governance.

### Relationships: How are the identified elements connected?

Element identifiers let engineering build a trace chain. Each relationship connects identified elements and states what the connection means.

```yaml
source_element_id: RTM-PAYMENT-REQ-018
relationship: implemented_by
target_element_id: ARTIFACT-PAYMENT-CLIENT
```

The traceability layer does not force every system to replace its native IDs with one global numbering scheme. It establishes which identifier serves as the Trace ID for each governed element, preserves mappings where needed, and records relationships among them.

[[M_EBG_A_03-2.png]]

### Evidence: What supports the connection?

When a relationship makes a governance claim, link the evidence that supports it. An RTM link may be maintained as a declared relationship; Development Evidence may show that a rule was delivered or a decision occurred. Audit can distinguish a declared link from one that is observed and verified.

```yaml
relationship: constrained_by
source_element_id: DECISION-EXEC-042
target_element_id: RULE-PAYMENT-IDEMPOTENCY
evidence_ref: EVD-DECISION-042
```

This is the division of labor between Articles 02 and 03:

```text
Article 02: What observable decision behavior was captured?
Article 03: How are governance-relevant elements identified and connected, and which changing states matter?
```

---

## 5. Engineering Fine-Grained Traceability

The engineering design begins at creation time.

Anchor Architecture describes an Anchor as a spatiotemporal coordinate that binds identity, location, and temporal state. That principle is useful here: a state that was not identifiable when created is difficult to recover later without speculation.

The Traceability Engineering Element applies that principle across governance-relevant elements. Stable identifiers establish which elements are being referred to; state attributes such as role, version, timestamp, and status are recorded where needed; explicit relationships connect the elements into trace chains.

### Capture the smallest meaningful unit

Do not assign one Trace ID to an entire project and call the work traceable. Also do not turn every token into a governance record.

Use the smallest unit that can be independently judged or changed.

For the payment retry example, these may be separate identified elements:

```text
Context delivery
Retry-strategy decision
Idempotency-rule invocation
Generated implementation change
Verification result
Architecture-scope finding
```

They can share a parent change reference while retaining their own Trace IDs. A native identifier from an RTM, workflow, evidence, or repository system can serve that purpose if it resolves consistently; otherwise, maintain an explicit mapping.

### Keep the ID stable and the record appendable

The identifier should identify the element, not describe its entire current state. Role, version, timestamp, status, and other changing values belong in state records or structured attributes.

If a trace is corrected, retain the earlier record and append a new record version. Do not silently rewrite the past. If one engineering state replaces another, express `superseded_by` or another explicit relationship.

### Preserve both hierarchy and non-hierarchical links

Parent-child relationships are useful, but engineering work is not always a tree. One rule may constrain several decisions. One decision may affect several artifacts. One test may verify several changes.

The model therefore needs both:

```text
parent_element_id
    structural containment or sequence

relationships[]
    typed links across the wider engineering graph
```

This is one place where runtime tracing offers a useful lesson. OpenTelemetry uses parent relationships for nested operations and links for related spans that do not fit one parent-child tree. Development traceability needs similar flexibility, while connecting engineering elements such as RTM items, operation records, decision executions, rules, evidence, and artifacts.

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

- duplicate or missing element identifiers;
- unresolved references across RTM, operation, decision, evidence, and artifact systems;
- state attributes missing when required by a specific governance question;
- mutable references whose historical state cannot be resolved;
- timestamps that violate a claimed sequence, when time is relevant;
- relationships whose source, target, type, or evidence cannot be established;
- incompatible schema versions;
- orphaned evidence;
- an operation or generated result with no trace back to its decision basis.

Having Trace IDs does not mean the work has been governed. It means the organization has engineered units that can be followed and checked.

```text
Engineering creates traceable units
Evidence supports observed states and relationships
Audit checks trace integrity and claims
Governance judges and acts
```

That distinction keeps the PDCA loop concrete:

```text
Plan: define which elements need identifiers, which changing states matter, and which relationships must be traceable
Do: identify elements and record relevant states and links as engineering work occurs
Check: audit identity resolution, state history, relationship chains, and evidence coverage
Act: correct broken links, improve capture, or reject unsupported governance claims
```

---

## 6. Example: Tracing One Payment Retry Decision Beyond Documents and Code

Now return to the Development Evidence from Article 02.

The change is still associated with one parent development activity, but each governance-relevant element has an identifier that can be connected to the others. Existing IDs from RTM and workflow systems remain usable as element identifiers.

```yaml
trace_chain:
  root_element:
    element_id: CHANGE-PAYMENT-RETRY-184
    element_type: development_change

  elements:
    - element_id: RTM-PAYMENT-REQ-018
      element_type: requirement
      state:
        version: v2
        status: approved

    - element_id: OP-PAYMENT-RETRY-184
      element_type: operation
      state:
        timestamp: 2026-09-30T10:20:00+08:00
        role: system-design

    - element_id: DECISION-EXEC-042
      element_type: decision_execution
      state:
        timestamp: 2026-09-30T10:24:18+08:00
        role: system-design

    - element_id: RULE-PAYMENT-IDEMPOTENCY
      element_type: rule
      state:
        version: v4
        status: active

    - element_id: EVD-DECISION-042
      element_type: development_evidence
      state:
        timestamp: 2026-09-30T10:24:20+08:00
        status: captured

    - element_id: ARTIFACT-PAYMENT-CLIENT
      element_type: code_artifact
      state:
        version: git:8f2a1c7

    - element_id: TEST-PAYMENT-RETRY-031
      element_type: verification_result
      state:
        timestamp: 2026-09-30T10:31:00+08:00
        status: passed

  relationships:
    - source: RTM-PAYMENT-REQ-018
      type: assigned_to
      target: OP-PAYMENT-RETRY-184

    - source: OP-PAYMENT-RETRY-184
      type: contains_execution
      target: DECISION-EXEC-042

    - source: DECISION-EXEC-042
      type: constrained_by
      target: RULE-PAYMENT-IDEMPOTENCY
      evidence: EVT-rule-trigger-021

    - source: DECISION-EXEC-042
      type: recorded_by
      target: EVD-DECISION-042

    - source: DECISION-EXEC-042
      type: generated
      target: ARTIFACT-PAYMENT-CLIENT
      evidence: EVT-code-generation-026

    - source: ARTIFACT-PAYMENT-CLIENT
      type: verified_by
      target: TEST-PAYMENT-RETRY-031
      evidence: EVT-test-result-031
```

Notice that `role`, `version`, `timestamp`, and `status` are present only where they describe a relevant state. The requirement has a version and approval status. The operation and decision execution have timestamps and roles. The rule has a version and active status. The artifact points to a Git state. The verification result has a timestamp and outcome.

The RTM requirement, Operation, Decision Execution, Evidence, artifact, and test each have a Trace ID. Where a system already supplies a reliable native ID, that ID can serve as the Trace ID; otherwise, the mapping must be explicit. Their relationships form the trace chain.

That makes several audits possible without pretending to know the model's hidden reasoning:

```text
Identity audit
    Can the RTM requirement, operation, decision execution, evidence, artifact, and test all be resolved?

Version audit
    Did it use the rule and context versions valid at that time?

Temporal audit
    Did the rule invocation occur before the generated change?

Relationship audit
    Does the RTM-to-operation-to-decision-to-artifact-to-test chain resolve, and is the rule link supported?

Continuity audit
    Can the later verification and correction be followed from the original decision?
```

An identifier does not decide whether the retry strategy is acceptable. A role does not grant authority by itself. A version does not prove correctness. A timestamp does not prove causality. Evidence does not make every relationship true.

Together, stable element identities, relevant state, typed relationships, and evidence create an inspectable trace chain upon which Audit can operate and governance can make a supportable judgment.

> Evidence makes behavior observable. Traceable identifiers let engineering elements be connected. Role, version, timestamp, and status preserve the state when it matters. Governance still begins when Audit evaluates those relationships and an authorized process acts on the findings.

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
