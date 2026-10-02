# You Cannot Govern an AI Development Run If Its Prompt and Context Disappear

## A visible prompt is not the complete development basis, and a surviving code change does not prove what the agent received.

**Engineering Before Governance | 04 / 08**

[[M_EBG_A_04-0.png]]

An engineer asks an AI agent to change the retry behavior of a payment service:

> Add one retry for temporary payment failures. Do not change the public API. Preserve the existing idempotency behavior. Run the payment integration tests.

The agent reads several files, follows repository instructions, changes the implementation, and reports that the tests passed.

Two weeks later, the code and pull request still exist. The original prompt may even remain in the conversation history.

But the team cannot answer:

- Which payment specification version did the agent receive?
- Were the business, system design, and architecture constraints all present?
- Which repository rules and source files entered the effective context?
- Was part of the conversation summarized or truncated?
- Which model, tools, permissions, and environment produced the change?
- Did the agent remain inside the approved Change Scope?

The code survived. The engineering basis that produced it did not.

That is the governance problem:

> If the prompt and effective context of an AI development run are transient or unidentifiable, the organization can inspect the result but cannot reliably judge whether the run used the required system state and approved change boundary.

---

## 1. Governance Problem: The Visible Prompt Is Only Part of the Basis

When a result goes wrong, the first question is often: "What prompt did we give the agent?"

That is a reasonable place to start. It is just not the whole story.

The visible request may be joined by system instructions, repository guidance, business and architecture specifications, source files, retrieved documentation, earlier conversation turns, generated summaries, tool results, permissions, and the model version interpreting all of them.

This means two runs can receive the same visible prompt and still work from different engineering realities.

```text
Same visible prompt
    + different effective context
    = different development basis
```

One run may receive the current architecture constraint. Another may retrieve an obsolete copy. One may include the full conversation. Another may receive a compressed summary after the context window fills.

This is also why "the file was in the repository" is not enough. We need to know which of four things actually happened:

```text
Available: the system could provide it
Delivered: it entered the effective context
Accessed: the agent or tool read it
Claimed: someone says it influenced the result
```

A conversation transcript helps, but it may still omit hidden instructions, retrieval results, permissions, or context transformations.

Again, we are not trying to reconstruct the model's mind. We are trying to preserve the external engineering basis well enough that someone else can later inspect it.

---

## 2. Existing Solutions Preserve Parts of the Basis

The good news is that teams already preserve many useful pieces of an AI-assisted development run.

Git preserves repository state, source history, and the difference between revisions. It can recover the files that existed at a commit.

Specification-Driven Development moves intended work out of a transient conversation and into persistent artifacts. Current approaches vary, but commonly retain requirements, design, plans, tasks, proposals, or change specifications.

That is an important step:

```text
Intent only in chat
    -> the session ends
    -> the basis is difficult to recover

Intent in a versioned specification
    -> the session ends
    -> recorded intent remains inspectable
```

[[M_EBG_A_04-1.png]]

Conversation history preserves visible interaction. Agent telemetry can preserve selected requests, responses, tool calls, retrieval activity, and model identity. Tests and reviews preserve verification results.

So we already have a useful stack:

- Git preserves repository state.
- SDD preserves the intended change.
- Conversation history preserves visible interaction.
- Telemetry preserves selected development events.
- Tests and review preserve verification.

What is missing is not one more document. It is a reliable way to say which versions from this stack came together in this particular development run.

---

## 3. What Existing Solutions Still Cannot Resolve

This is where the gaps between the layers begin to matter.

Git can recover a file version, but it cannot prove that the version entered the agent's context.

SDD keeps intended work from disappearing, but the existence of a specification does not prove which version governed a run. A change specification may also describe only the current modification, not the full business, system design, and architecture state needed to interpret it.

A conversation transcript can show visible messages while omitting hidden instructions, context assembly, retrieval, permissions, or truncation. Telemetry can show that a tool was called without showing whether the call was allowed by the approved Scope.

A passing test proves only that the configured check passed. It does not prove that every required viewpoint or constraint was present when the code was designed.

In other words, the records survive, but they survive in separate places:

```text
Specification
Conversation
Repository state
Tool trace
Test result
Approval
```

And the team is still left with one very practical question:

> Which versioned system state and bounded change state were actually supplied to this development run, and what evidence supports that claim?

This is the **Versioned Development Basis Gap**.

---

## 4. Governance Scope and the Elements That Must Become Visible

Let us narrow the problem before adding more structure. This article stays inside the software development stage and looks at one identifiable AI-assisted development run.

It does not attempt to expose private model reasoning or govern every decision inside the run. Individual choices still receive their own Decision IDs and Decision Behavior Evidence, as discussed in Article 02.

Instead of starting with a long list of fields, we can group the required Governance Engineering Elements around three questions any reviewer would naturally ask.

### What should the run receive?

The **Prompt Artifact** preserves the requested change, constraints, acceptance conditions, author, approval state, and version.

The **System Basis Reference** points to the relevant VSS version. VSS represents the system across viewpoints such as PM/BA business analysis, system design, and system architecture.

The **Change Scope** identifies the bounded modification: what may change, which interfaces and constraints apply, and what remains outside the task.

### What did the run actually receive?

The **Context Manifest** identifies the instructions, specifications, source artifacts, tools, permissions, and environment delivered to the run. It also records important transformations: content that was omitted, summarized, truncated, retrieved, or replaced.

### What connects the basis to the result?

A stable **Development Change ID** and **Trace ID** connect the Prompt Artifact, Context Manifest, Decision IDs, tool events, changed artifacts, tests, and review.

[[M_EBG_A_04-2.png]]

Put together, these elements give us a recoverable snapshot of the development basis:

```text
VSS version
    the relevant system state

Scope version
    the approved change boundary

Prompt Artifact
    the governed request

Context Manifest
    the delivered development conditions

Trace ID
    the connection to decisions, actions, and evidence
```

Their existence makes governance possible. It does not mean governance has already happened.

---

## 5. Engineering the Development Basis and Audit

The important shift is that we build this basis before the agent changes code, not after someone asks for an audit.

### Define the expected basis

VSS describes the relevant system state. Scope selects the part involved in this change. Applicable rules determine which viewpoints, constraints, artifacts, capabilities, and approvals are mandatory.

```text
VSS + Scope + applicable rules
    -> expected development basis
```

For the payment retry change, that may mean the business rule for temporary failures, the system design for retry limits, the architecture rule for transaction boundaries, and the approved files inside Scope. Now the expected basis is concrete enough to check.

### Capture the observed basis

The Prompt Artifact and Context Manifest need stable identities and versions. Large or sensitive content can stay in controlled storage while the manifest keeps its identifier, version, integrity hash, and access classification.

The development environment should capture which versions were resolved, which rules and files were delivered, which tools and permissions were active, and whether context was summarized or truncated.

Will this reproduce the exact same output every time? Probably not. Models and external tools may still be non-deterministic. The more practical goal is **basis reproducibility**: a reviewer can recover the controlled inputs and conditions against which the run should be judged.

```text
Context Manifest + development evidence
    -> observed development basis
```

### Compare expected and observed

Now Audit has something concrete to compare: what should have been present and what the evidence says was actually present.

```text
Expected basis: VSS + Scope + rules
Observed basis: Context Manifest + evidence
Audit finding: matched, missing, stale, conflicting, out of scope, or unknown
```

This comparison can reveal that an architecture viewpoint was missing, an obsolete specification was delivered, a summary removed a constraint, or an agent modified an artifact outside Scope.

[[M_EBG_A_04-3.png]]

There is one boundary worth keeping clear. VSS, Scope, Context Manifests, Trace IDs, and Evidence do not approve or reject a change. Even Audit produces a finding, not the final judgment.

Governance still requires an applicable rule, sufficient evidence, an authorized role, and an action.

```text
Engineering creates the expected and observed states
Evidence supports the observed state
Audit identifies the difference
Governance judges and acts
```

That separation makes the loop repeatable:

```text
Plan: define the required basis and controls
Do: develop under an identified, versioned basis
Check: compare evidence with VSS, Scope, and rules
Act: accept, reject, correct, escalate, or improve the controls
```

---

## 6. Example: Auditing a Payment Retry Development Change

With that in place, the payment retry request no longer has to be remembered as a conversation. It can be reviewed as an identifiable development change.

```yaml
development_change:
  id: CHG-payment-retry-184
  trace_id: TRACE-payment-retry-184
  prompt: PROMPT-payment-retry@v3
  context: CTX-payment-184@v1

expected_basis:
  vss: VSS-payment-system@v12
  viewpoints:
    - business-analysis
    - system-design
    - system-architecture
  scope: SCOPE-payment-retry@v4
  constraints:
    - maximum-one-retry
    - preserve-idempotency
    - preserve-public-api
    - preserve-transaction-boundary

observed_basis:
  business-analysis:
    status: observed
    evidence: EVT-context-delivery-101
  system-design:
    status: observed
    evidence: EVT-context-delivery-102
  system-architecture:
    status: not-captured
  modified_artifacts:
    - ref: src/payment/client.ts
      evidence: EVT-file-write-211
    - ref: src/transaction/shared-boundary.ts
      evidence: EVT-file-write-212

audit:
  findings:
    - result: missing-required-basis
      detail: Architecture viewpoint was not evidenced as delivered.
    - result: out-of-scope-change
      detail: Shared transaction boundary was modified outside Scope.

governance_judgment:
  authority: human:payment-maintainer
  decision: reject-development-change
  actions:
    - restore the out-of-scope artifact
    - add the approved architecture viewpoint
    - rebuild the Context Manifest
    - repeat implementation and review
```

Notice what happened here. The Prompt Artifact did not govern the change. Neither did the Context Manifest or the Evidence.

What they did was make the comparison possible. Audit could see that a required architecture viewpoint was missing and that a file outside Scope had been modified. The authorized maintainer could then reject the change and require correction on a supportable basis.

The same Trace ID can connect this run to `CODE-DEC-042`, the individual decision to retry once. Article 02 shows what must be observed around that choice. Article 03 establishes the fine-grained, role-aware, versioned, and timestamped trace that connects it to other engineering elements. This article shows which versioned system state and Change Scope were available when it was made.

Engineering comes first because governance cannot compare, judge, or improve what engineering has not made visible.

---

## References

- [Kiro: Specs](https://kiro.dev/docs/specs/)
- [Kiro: Feature Spec best practices](https://kiro.dev/docs/specs/best-practices/)
- [GitHub Spec Kit](https://github.github.com/spec-kit/)
- [GitHub Spec Kit: Spec persistence models](https://github.com/github/spec-kit/blob/main/docs/concepts/spec-persistence.md)
- [OpenSpec: Spec-driven schema](https://openspec.dev/docs/schemas/spec-driven)
- [OpenSpec: Quickstart and archive model](https://openspec.dev/docs/quickstart)
- [OpenTelemetry: Generative AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/)
- [W3C PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/)
- [Decision Provenance: Harnessing Data Flow for Accountable Systems](https://www.repository.cam.ac.uk/items/14c68264-4c52-41d9-bf37-1dccc966cdcb)
- [NIST: Assurance Case](https://csrc.nist.gov/glossary/term/assurance_case)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)

### Related Work by the Author

- [Spark Tsai, *Ghost Intent: An Effect of Traceability Collapse in GenAI-Assisted SDLCs*](https://doi.org/10.5281/zenodo.18872540)
- [Spark Tsai, *Engineering Determinacy: Structuring Established Knowledge So That It Need Not Be Reinterpreted*](https://doi.org/10.5281/zenodo.22718019)
- [Spark Tsai, *Viewpoint-Structured Specification (VSS)*](https://doi.org/10.31224/6612)
- [Spark Tsai, *Scope as a Governance Primitive: Making Inference, Authority, Effect, and Evidence Explicit in AI Governance*](https://doi.org/10.5281/zenodo.22108234)
- [Spark Tsai, *Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development*](https://doi.org/10.31224/6616)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
