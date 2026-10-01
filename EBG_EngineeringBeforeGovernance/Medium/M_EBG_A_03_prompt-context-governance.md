# You Cannot Govern an AI Development Run If Its Prompt and Context Disappear

## A visible prompt is not the complete execution basis, and a surviving code change does not prove what the agent received

[[M_EBG_A_03-0.png]]

An engineer asks an AI agent to change the retry behavior of a payment service:

> Add one retry for temporary payment failures. Do not change the public API. Preserve the existing idempotency behavior. Run the payment integration tests.

The agent reads several files, follows repository instructions, inspects design material, changes the implementation, and reports that the tests passed.

Two weeks later, another engineer needs to modify the same behavior. The code is still in Git. The pull request is still available. The original prompt may still appear in a conversation history.

But the team cannot reliably answer:

- Which version of the payment specification did the agent receive?
- Were the business, system design, and architecture constraints all present?
- Which repository instructions and files were delivered or accessed?
- Was part of the conversation summarized or truncated?
- Which model, tools, permissions, and environment produced the change?
- Did the agent operate within the approved Change Scope?
- Which evidence can prove any of these claims?

The change survived. The engineering basis that produced it did not.

That is the governance problem:

> If the prompt and effective context of an AI development run are transient or unidentifiable, the organization can inspect the result but cannot reliably determine whether the run operated against the required system state and approved change boundary.

---

## 1. Governance Problem: The Effective Execution Basis Is Invisible

Teams often talk about "the prompt" as if it were the complete instruction given to an agent.

It rarely is.

The user prompt may describe the requested change, but the agent's effective execution basis can also include:

- system and organization instructions;
- repository-level agent guidance;
- business, system design, and architecture specifications;
- source files and tests selected for inspection;
- retrieved documentation or search results;
- earlier conversation turns and generated summaries;
- tool definitions and tool results;
- environment variables, permissions, and execution boundaries;
- the model and agent version interpreting those inputs.

Two runs can receive the same visible prompt and operate under different conditions. One may receive the current architecture rule; another may retrieve an obsolete copy. One may include the full conversation; another may receive a compressed summary after the context window fills.

```text
Same visible prompt
    + different effective context
    = different execution basis
```

A conversation transcript is useful, but it does not necessarily reveal every hidden instruction, retrieved artifact, permission, transformation, or version involved in the run.

It also collapses several different states:

```text
Available
    The system could provide the information

Delivered
    The information entered the agent's effective context

Accessed
    The agent or tool read the information

Claimed basis
    A human or agent says the information influenced the result
```

A file existing in the repository does not prove that it was delivered. Delivery does not prove access. A cited rule does not prove correct application. A generated rationale does not reveal private model reasoning.

The governance requirement is therefore not to reconstruct an AI's mind. It is to make the external engineering basis of the run identifiable, versioned, and supportable by evidence.

---

## 2. Existing Solutions Preserve Parts of the Basis

The industry is not starting from nothing. Several established practices preserve useful parts of an AI-assisted development run.

Git records repository state, source history, authorship metadata, and changes between revisions. It allows a team to recover the artifacts that existed at a commit and inspect what changed.

Specification-Driven Development, or SDD, moves intended work out of an ephemeral conversation and into persistent artifacts. Current tools use different structures, but commonly produce some combination of requirements, design, implementation plans, and tasks. Kiro uses requirements, design, and task artifacts. GitHub Spec Kit uses specifications, plans, and tasks. OpenSpec represents changes through proposals, delta specifications, design, and tasks.

This is an important engineering move:

```text
Intent only in conversation
    -> session ends
    -> intent becomes difficult to recover

Intent in a versioned specification
    -> session ends
    -> recorded intent remains inspectable
```

[[M_EBG_A_03-1.png]]

Conversation history preserves visible interaction. Agent telemetry can preserve selected model requests, responses, tool calls, retrieval activity, token usage, and runtime identity. Tests and reviews preserve verification results. Audit logs can preserve authenticated events and changes to controlled resources.

Each practice protects a useful layer:

- Git preserves repository state and change history.
- SDD preserves a structured statement of intended change.
- Conversation history preserves visible interaction.
- Telemetry preserves selected runtime events.
- Tests and reviews preserve verification results.

These are real solutions. The remaining problem is not that they have no value. It is that they do not automatically form one governed execution basis.

---

## 3. What Existing Solutions Still Cannot Resolve

Git can recover a file version, but it does not prove that the version entered the agent's context.

SDD prevents intended work from disappearing, but no single SDD format represents every relevant system viewpoint, and the existence of a specification does not prove which version governed a run.

A conversation transcript can show visible messages without exposing hidden instructions, context assembly, retrieval results, permissions, or truncation. Telemetry can show a tool call without explaining which approved Scope authorized it. A passing test can show that configured checks passed without proving that every applicable system constraint was present.

The records survive in separate layers:

```text
Specification
Conversation
Repository state
Tool trace
Test result
Approval
```

But the organization still lacks a reliable answer to:

> Which versioned system state and bounded change state were actually supplied to this run, and what evidence supports that claim?

This is the **Versioned Execution Basis Gap**.

The missing relationship is not merely another document. It is a traceable binding among the governed request, relevant system state, approved change scope, effective context, execution identity, and resulting evidence.

---

## 4. Governance Scope and the Elements That Must Become Visible

This article is limited to the software development stage.

Its governance unit is **one identifiable AI-assisted development run**. Its governance object is the external engineering basis supplied to that run and the transformations applied to that basis while the run is active.

It does not attempt to govern:

- private model reasoning;
- deployment or production operations;
- every engineering decision made during the run;
- the long-term business outcome of the resulting change.

Individual engineering decisions inside the run remain separate Decision IDs governed through the Decision Behavior Engineering Elements and Evidence introduced in the previous article.

For this governance problem, the required **Governance Engineering Elements** include:

### Prompt Artifact

A versioned representation of the governed request, including requested outcome, constraints, acceptance conditions, author, approval state, and integrity reference.

### Context Manifest

An identifiable manifest of the external instructions, artifacts, capabilities, and environmental conditions delivered to the run.

### Execution ID

A stable identity that binds the Prompt Artifact, Context Manifest, execution events, Decision IDs, resulting engineering artifacts, and verification evidence.

### System Basis Reference

A reference to the applicable version of the system state. In this series, VSS makes that state observable across PM/BA business analysis, system design, system architecture, and other required viewpoints.

### Change Scope

The approved boundary of the current change: what may be changed, what may be read, which interfaces and constraints apply, and what remains outside the task.

### Context State and Transformation Events

Evidence that identifies what was available, delivered, accessed, omitted, summarized, truncated, retrieved, or replaced during execution.

### Execution Capability State

The agent, model, tool, permission, environment, and instruction versions active for the run.

[[M_EBG_A_03-2.png]]

These elements establish a recoverable point-in-time basis:

```text
VSS Version
    relevant system state

Scope Version
    bounded change state

Prompt Artifact Version
    governed request

Context Manifest Version
    delivered execution conditions

Execution ID
    binding across actions, decisions, and evidence
```

They are infrastructure for governance. Their existence does not mean that governance has occurred.

---

## 5. Engineering the Execution Basis and Audit Mechanism

The engineering design begins before the agent executes.

### Build the expected basis

VSS and Scope define what the run is expected to receive.

VSS provides the relevant system state across required viewpoints. Scope identifies the bounded part involved in the current change. Rules determine which viewpoints, constraints, artifacts, capabilities, and approvals are mandatory for this type of run.

```text
VSS + Scope + Applicable Rules
    -> Expected Execution Basis
```

### Capture the observed basis

The Prompt Artifact and Context Manifest must use stable identities and versions. Large or sensitive content can remain in controlled storage while the manifest records its stable identifier, version, integrity hash, and access classification.

Context assembly should generate point-in-time evidence for:

- artifact resolution and version selection;
- instruction and rule delivery;
- file and source delivery or access;
- agent, model, tool, permission, and environment identity;
- context summary, truncation, retrieval, or replacement;
- start, end, and integrity metadata.

The result is not perfect output reproducibility. Models and external tools may remain non-deterministic. The practical goal is **basis reproducibility**: the organization can recover the controlled inputs and conditions against which the run should be reviewed or repeated.

```text
Context Manifest + Execution Evidence
    -> Observed Execution Basis
```

### Use Evidence to audit VSS and Scope

The Evidence model from the previous article provides the distinction required for a credible audit:

- `observed`: captured directly as an event or state;
- `declared`: stated by a human or agent;
- `derived`: inferred from identified evidence;
- `verified`: independently checked against a rule or artifact.

A Context Manifest entry is execution evidence. When it is connected to a specific Decision ID and supports a claim about that decision's input basis, it also becomes relevant Engineering Decision Behavior Evidence.

The audit mechanism compares the normative state with the observed state:

```text
Expected Execution Basis
    VSS + Scope + Rules

Observed Execution Basis
    Context Manifest + Execution Evidence

Audit
    compare expected and observed states

Audit Finding
    compliant, missing, stale, out of scope, conflicting, or unknown
```

The comparison can determine whether a required viewpoint was missing, an obsolete specification was delivered, a context summary removed a constraint, a tool exceeded Scope, or an unapproved model or permission set was used.

[[M_EBG_A_03-3.png]]

### Infrastructure is not governance

VSS, Scope, Prompt Artifacts, Context Manifests, Trace IDs, and Evidence do not approve or reject a run by themselves. They make the relevant states available for evaluation.

An Audit Finding is also not automatically the final Governance Judgment. Governance still requires an applicable rule, an authorized role or control, an evaluation of evidence strength, and an action.

```text
Engineering
    creates identifiable expected and observed states

Evidence
    supports claims about the observed state

Audit
    identifies correspondence or difference

Governance
    applies rules and authority to judge and act
```

For deterministic rules, an authorized control may automatically block a run when a mandatory context element is missing. For semantic or risk-based questions, the Audit Finding may require human review.

This produces a repeatable governance loop:

```text
Plan
    Define the required VSS, Scope, context, evidence, and controls

Do
    Execute under an identified and versioned basis

Check
    Audit Evidence against VSS, Scope, and Rules

Act
    Accept, reject, correct, escalate, or improve the engineering controls
```

This is what **Engineering Before Governance** means. Engineering creates the observable states and evidence infrastructure that governance needs. Evidence makes a judgment supportable. Audit turns comparison into a finding. Governance remains the separate act of authorized judgment and control.

---

## 6. Example: Auditing a Payment Retry Development Change

The payment retry request can now be represented as a governed development change rather than a remembered conversation. The example remains entirely inside the development stage: defining the change, assembling the development context, modifying code, and reviewing the result.

```yaml
development_change:
  id: CHG-payment-retry-184
  phase: development
  trace_id: TRACE-payment-retry-184
  prompt_artifact: PROMPT-payment-retry@v3
  context_manifest: CTX-payment-184@v1

expected_development_basis:
  vss: VSS-payment-system@v12
  required_viewpoints:
    - business-analysis
    - system-design
    - system-architecture
  scope: SCOPE-payment-retry@v4
  required_constraints:
    - retry-temporary-failures-only
    - maximum-one-retry
    - preserve-idempotency
    - preserve-public-api
    - preserve-transaction-boundary

observed_development_basis:
  prompt_artifact:
    version: v3
    status: verified
    evidence: EVT-prompt-approval-031
  delivered_viewpoints:
    business-analysis:
      version: v12
      status: observed
      evidence: EVT-context-delivery-101
    system-design:
      version: v12
      status: observed
      evidence: EVT-context-delivery-102
    system-architecture:
      status: not-captured
  scope:
    version: v4
    status: observed
    evidence: EVT-context-delivery-104
  modified_artifacts:
    - ref: src/payment/client.ts
      status: observed
      evidence: EVT-file-write-211
    - ref: src/transaction/shared-boundary.ts
      status: observed
      evidence: EVT-file-write-212

audit:
  findings:
    - id: FINDING-CONTEXT-001
      result: missing-required-basis
      detail: System architecture viewpoint was not evidenced as delivered.
    - id: FINDING-SCOPE-002
      result: out-of-scope-change
      detail: Shared transaction boundary was modified outside approved Scope.

governance_judgment:
  authority: human:payment-maintainer
  decision: reject-development-change
  evidence_strength: sufficient
  actions:
    - mark the current development change as not acceptable
    - restore the out-of-scope artifact
    - add the approved architecture viewpoint to the development context
    - rebuild the Context Manifest
    - repeat implementation and review under a new Development Change ID
```

The Prompt Artifact did not govern the development change. The Context Manifest did not govern the development change. The Evidence did not govern the development change.

Together, they allowed Audit to compare the VSS-and-Scope expectation with the observed development basis. The findings then allowed an authorized maintainer to make a supportable Governance Judgment about the change and require corrective action before the code could be accepted.

The same Trace ID can connect this development change to individual Decision IDs. For example, the decision to retry once can reference `CODE-DEC-042`, while its Decision Behavior Evidence references the Prompt Artifact, Context Manifest, applicable constraints, selection event, and realized code artifact.

The relationship is now explicit:

```text
VSS and Scope
    define what should be true

Development Evidence
    shows what can be demonstrated during the change

Audit
    identifies the difference

Governance Judgment
    determines what must happen next
```

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
