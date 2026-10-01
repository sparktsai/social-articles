# When the Prompt Disappears, What Is Left to Govern?

## The first governance problem in AI-assisted development is that its governing intent may exist only inside a conversation

[[M_EBG_A_02-0.png]]

An AI development task often begins with a prompt:

Build this feature. Do not change that interface. Follow this architecture. Stay within these files. Run these tests.

Inside the conversation, those instructions appear to govern the work.

Then the session ends.

The code remains, but the prompt may be difficult to retrieve. Parts of the context may have been summarized, truncated, or carried implicitly by the person directing the work. A later reviewer can inspect the result without being able to identify the complete intent, scope, constraints, and acceptance conditions under which it was produced.

This is the first governance problem:

> If the conditions governing AI development exist only in a prompt, the governance object can disappear with the conversation.

Specification-Driven Development, or SDD, provides an important engineering response. To understand how far that response goes, we first need to examine how SDD is currently practiced, what it makes possible, and which governance questions it still leaves open.

---

## The Current State of SDD

SDD does not currently have one standardized format. Different tools define different files, structures, and lifecycles, but a common pattern has emerged:

```text
Requirements
    -> Design
    -> Tasks
    -> Implementation
```

Kiro, for example, produces `requirements.md`, `design.md`, and `tasks.md`. GitHub Spec Kit commonly uses `spec.md`, `plan.md`, and `tasks.md`. OpenSpec represents a proposed change through a proposal, delta specifications, design, and tasks.

Most current implementations share several practical characteristics:

- specifications are usually natural-language Markdown artifacts;
- work is organized around a feature or change rather than one complete system document;
- AI commonly generates the first draft from a human request and repository context;
- humans review, correct, or approve the artifacts before or during implementation;
- the specification files are stored with the project and can be versioned with Git.

These conventions are becoming common, but they are not yet a shared SDD standard. Each tool still decides what a specification contains, how long it remains authoritative, and how it relates to implementation.

---

## What SDD Solves

Despite those differences, current SDD tools make the same important engineering move:

> The intended work becomes an artifact rather than remaining only in conversation.

This matters for governance.

Once a specification exists as a file, it can be reviewed, versioned, compared, approved, and connected to implementation work. When committed with Git, it becomes possible to inspect what the recorded requirements and design looked like at an earlier point in development.

At minimum, SDD addresses a real failure mode of prompt-based development:

```text
Intent in prompt
    -> session ends
    -> intent becomes difficult to recover
```

becomes:

```text
Intent in specification
    -> specification is versioned
    -> recorded intent can be recovered
```

That is already an important engineering foundation for governance.

[[M_EBG_A_02-1.png]]

---

## What Git Adds -- and What It Does Not

If the specification is committed before implementation, Git can help answer questions such as:

- What problem was recorded at the time?
- What requirements and acceptance criteria existed?
- What design was proposed?
- How was the work divided into tasks?
- Which requirements were changed later?
- Which code change accompanied a specification change?

But the wording here matters.

SDD with Git can recover the **recorded specification state at the time**.

It does not necessarily recover the **complete execution state at the time**.

A repository may contain the correct version of `spec.md`, but that alone does not prove:

- that the agent loaded that version;
- which parts of the specification entered its context;
- whether the context was truncated or summarized;
- which project instructions or behavioral rules were active;
- which model, tools, permissions, and environment were used;
- which actions the agent actually performed;
- which tests were run and what evidence they produced.

This gives us an important distinction:

> Specification history is not the same as execution history.

SDD makes intended state more durable. Git makes changes to that recorded state recoverable. Governance still needs a way to bind that intended state to actual execution.

---

## What SDD Still Leaves Unresolved

Once development intent has been externalized and versioned, several governance problems become easier to see. They are not evidence that SDD has failed. They mark the boundary between preserving a specification and proving how that specification governed a development run.

### Does the Specification Describe the System or the Change?

Another problem appears as soon as specifications become persistent.

Is a specification supposed to describe the entire system, or only the part being changed?

In current SDD practice, it is usually closer to the second.

Most tools organize specifications around a feature or change. This keeps the working context manageable and gives the agent a bounded task. OpenSpec makes the distinction particularly explicit: current system behavior is maintained as a specification baseline, while each proposed modification is represented as a delta. After implementation, the delta can be incorporated into the baseline and archived as part of the change history.

This suggests that an enterprise system needs three related layers rather than one document called "the specification":

```text
System Specification
    The observable specification of the system as a whole

Change Scope
    The part of that system involved in the current change

Versioned Execution Basis
    The exact system version and change scope governing a run
```

These are not interchangeable.

A system-wide specification may be too large for one agent run. A change scope may omit unchanged constraints that still apply. An execution basis must therefore identify both the system state from which the change begins and the bounded region in which the change is allowed to operate.

The existence of a feature specification therefore does not yet tell us how the current change relates to the system as a whole, or which exact system state governed a particular execution.

---

### Who Produced and Authorized the Specification?

Modern SDD tools commonly let AI generate the first draft.

A human provides a feature request or problem statement. The AI expands it into requirements, edge cases, acceptance criteria, design, and implementation tasks. In more controlled workflows, a human reviews each stage before the next stage begins. In faster workflows, the tool may generate all artifacts in one pass.

This changes specification work from purely human authorship to mixed authorship:

```text
Human intent
    -> AI-generated specification draft
    -> human review and correction
    -> approved development basis
```

The useful governance question is not simply whether a human or AI wrote the text.

It is:

> Who had the authority to define, interpret, and approve each part of the specification?

AI can identify likely edge cases. It can formalize acceptance criteria. It can inspect an existing repository and propose a design. But an AI-generated assumption does not become an authorized business decision merely because it appears in a structured document.

AI may author a specification artifact. It does not automatically own the authority behind that specification.

---

### Which Engineering Viewpoints Formed the Specification?

SDD specifications often contain user stories, actors, or stakeholder statements. This provides useful context, but it does not necessarily preserve the distinct engineering viewpoints through which system intent is analyzed and constrained.

Consider the same payment change viewed through three different roles:

- **PM/BA -- Business Analysis:** What business problem is being solved? Which actors, business rules, outcomes, and functional requirements define success?
- **SD -- System Design:** How should system responsibilities, interactions, data flows, states, and failure behavior be designed to realize those requirements?
- **CA -- System Architecture:** Which architectural boundaries, component responsibilities, dependency directions, integration constraints, and system qualities must the design preserve?

These are not three descriptions of the same thing. They are different governing perspectives over the same system intent.

An AI can be assigned each role and produce an independent Viewpoint Artifact. The value comes from keeping those outputs structurally distinct before reconciling them. A PM/BA requirement may imply a workflow that the SD viewpoint cannot realize without changing system behavior. An SD design may introduce a dependency that the CA viewpoint prohibits. Those tensions already exist in the intent; multi-viewpoint structuring makes them visible before implementation.

If the outputs are instead merged immediately into one feature document, several governance questions remain unanswered:

- Which viewpoint produced each specification element?
- Which business requirement led to a particular system design decision?
- Which architecture constraint limits or rejects that design?
- Which conflicts between PM/BA, SD, and CA remain unresolved?
- Which elements from each viewpoint are included in the Scope of this change?
- Which required viewpoints were omitted for this change?

These questions cannot be answered merely by adding more prose to the same document. Governance needs the relevant parts of the specification to be identifiable, attributable, and selectable.

---

## Where VSS Begins

This is where Viewpoint-Structured Specification, or VSS, addresses a different problem from SDD.

Current SDD practice usually organizes intent around a feature or change. VSS instead represents the specification of the system as a whole, structured so that elements produced through PM/BA, SD, CA, and other risk-relevant engineering viewpoints remain independently identifiable.

The system-wide view does not need to be one enormous document. It can be a composed specification whose elements have stable identities and explicit relationships. Business analysis, system design, system architecture, test intent, and other engineering concerns can remain distinct while still contributing to one observable system state.

Conceptually:

```text
SDD
    The current feature or change is made explicit.

VSS
    The specification of the whole system is observable
    across identifiable viewpoints and elements.
```

VSS is therefore not simply another template for writing a feature specification. It provides the larger reference state against which an individual change can be located and evaluated.

[[M_EBG_A_02-2.png]]

---

## Scope Defines the Current Change

If VSS represents the system-wide specification, Scope identifies the region involved in the current change.

Scope can state:

- which VSS elements are included in the change;
- which elements are explicitly outside the change;
- which viewpoints and constraints apply;
- which interfaces, artifacts, or decisions may be modified;
- which surrounding system conditions must remain unchanged;
- which effects are expected or prohibited.

The relationship is:

```text
VSS
    The observable specification of the whole system

Scope
    The bounded change within that system
```

This distinction matters because a feature-level SDD artifact can describe what the team wants to build without fully showing where that change sits inside the larger governed system. Scope connects the local change to the system-wide specification and makes its boundary explicit.

---

## Version Makes the Past State Observable

VSS and Scope become historically useful when both are versioned.

For example:

```text
VSS version 42
    The observable system specification before the change

Scope CHG-142 version 3
    The approved boundary and requirements for this change

VSS version 43
    The observable system specification after the approved change
```

This makes two forms of observation possible.

First, the current VSS version provides an observable view of the system as a whole. Second, the combination of an earlier VSS version and a Scope version allows the organization to reconstruct the engineering state against which a past change was planned and governed.

Version does not preserve every detail of execution. It does establish the exact specification state and change boundary that an execution should have used.

---

## From VSS, Scope, and Version to TraceID

Even a well-structured specification does not prove that an agent followed it.

Suppose the Scope for a development run includes:

```text
VSS-PMBA-014   Business rule for retrying a failed payment
VSS-SD-009     Payment state transition and failure flow
VSS-CA-021     Dependency boundary for the payment service
```

VSS makes those system-level governance objects identifiable. Scope states that these elements, at specific versions, form the bounded basis of the current change.

The next requirement is continuity.

The versioned Scope must remain connected to the execution, the resulting artifacts, the verification evidence, and the final decision. This is the role a TraceID can begin to play.

```text
VSS Version
        -> Scope and Scope Version
        -> TraceID
        -> Agent Run
        -> Tool Actions
        -> Code Changes
        -> Tests and Reviews
        -> Approval or Exception
```

[[M_EBG_A_02-3.png]]

With this relationship, an organization can begin to ask a much stronger question:

> Which agent, operating under which authority and constraints, used which specification elements to produce this change, and what evidence supports the result?

This is no longer only documentation. It is the beginning of an engineering-visible governance chain.

---

## TraceID Is Not Evidence

A TraceID must not be confused with proof.

An identifier can connect records. It cannot guarantee that the records are complete, accurate, or trustworthy.

```text
TraceID != Evidence

TraceID = the connective key through which evidence can be found
```

For the trace to support governance, the connected records still need meaningful content:

- the VSS version, Scope version, and specification elements included in that Scope;
- the actor or agent responsible for the run;
- the authority and permissions under which it operated;
- the active rules and development constraints;
- relevant tool calls and resulting effects;
- source changes and generated artifacts;
- test, review, and policy-check results;
- approvals, rejections, and exceptions;
- timestamps and integrity controls.

VSS defines and organizes the system-wide governance objects. Scope identifies the current governed change. Version preserves the applicable state at that point in time. TraceID maintains continuity across engineering stages. Evidence records what actually happened. Governance mechanisms then use that state to constrain, evaluate, audit, and improve the workflow.

None of these elements is sufficient alone.

---

## The Difference Between Having a Specification and Being Governable

The progression can now be stated more precisely:

```text
Prompt
    Carries intent during an interaction

SDD
    Externalizes intent into persistent engineering artifacts

SDD + Git
    Preserves recorded specification history

VSS
    Makes the system-wide specification observable across viewpoints

Scope + Version
    Defines the current change and preserves its point-in-time basis

VSS + Scope + Version + TraceID
    Connects system intent and change boundaries to execution and evidence

Governance Engineering
    Uses that visible state for control, review, audit, and improvement
```

This is why engineering comes before an operational governance judgment.

The governance requirement may already exist. An organization may already require security review, authorized scope, human approval, traceability, or audit evidence. But those requirements cannot evaluate a concrete AI development run until engineering has produced the state on which the evaluation depends.

SDD is an important step because it prevents intended work from disappearing with the prompt.

VSS addresses the next problem: what did the system as a whole look like across its relevant viewpoints?

Scope addresses another: what bounded part of that system was involved in this change?

Version fixes both the system state and change boundary at the relevant point in time.

TraceID then addresses continuity: how does that versioned Scope remain connected to what the agent actually did?

Together, they move AI-assisted development from remembered instruction toward governable engineering state.

But they also expose the next question:

> Once a trace exists, what must be recorded before that trace can support monitoring, audit, and repeatable governance?

That is where traceability must become evidence.

---

## References

- [Kiro: Specs](https://kiro.dev/docs/specs/)
- [Kiro: Feature Spec best practices](https://kiro.dev/docs/specs/best-practices/)
- [GitHub Spec Kit](https://github.github.com/spec-kit/)
- [GitHub Spec Kit: Spec persistence models](https://github.com/github/spec-kit/blob/main/docs/concepts/spec-persistence.md)
- [OpenSpec: Spec-driven schema](https://openspec.dev/docs/schemas/spec-driven)
- [OpenSpec: Quickstart and archive model](https://openspec.dev/docs/quickstart)
