# You Cannot Govern an AI Development Run If Its Prompt and Context Disappear

## Prompts and context are execution inputs, but most teams still treat them as disposable conversation

[[M_EBG_A_02-0.png]]

An engineer asks an AI agent to change the retry behavior of a payment service.

The prompt appears clear:

> Add one retry for temporary payment failures. Do not change the public API. Preserve the existing idempotency behavior. Run the payment integration tests.

The agent reads several files, follows repository instructions, inspects an architecture document, edits the implementation, and reports that the tests passed.

Two weeks later, a production incident leads the team back to that change. The code is still in Git. The pull request is still available. The original prompt might still be somewhere in a chat history.

But the team cannot reliably answer:

- Which version of the architecture document did the agent read?
- Which repository instructions were active?
- Did the agent receive the idempotency constraint before or after it proposed the design?
- Was part of the conversation summarized or truncated?
- Which files were actually loaded into context?
- Which model, tools, permissions, and environment produced the change?
- Did "tests passed" refer to the full integration suite or a selected command?

The change survived. The engineering conditions that produced it did not.

That is the governance problem:

> If the prompt and effective context of an AI development run are transient, the organization can inspect the result but cannot reliably reconstruct the basis on which the result was produced.

Before an organization can govern an AI-assisted development run, it must first engineer the prompt and context into observable, versioned, and traceable execution inputs.

---

## A Prompt Is Only the Visible Part of the Instruction

Teams often talk about "the prompt" as if it were the complete instruction given to an agent.

It rarely is.

The user prompt may describe the requested change, but the agent's effective instruction can also include:

- system and organization instructions;
- repository-level agent guidance;
- specifications and architecture documents;
- source files and tests selected for inspection;
- retrieved documentation or search results;
- earlier conversation turns and generated summaries;
- tool definitions and tool results;
- environment variables, permissions, and execution boundaries;
- the model and agent version interpreting those inputs.

Together, these form the context in which the run operates.

The distinction matters because two runs can receive the same user prompt and still act differently. One may load the current architecture rule; another may retrieve an obsolete copy. One may have permission to modify a migration; another may not. One may include the full conversation; another may receive a compressed summary after the context window fills.

```text
Same prompt
    + different context
    = different execution basis
```

Prompt governance alone is therefore too narrow. The object that needs to become observable is the **effective execution context**: the identifiable set of instructions, artifacts, capabilities, and environmental conditions delivered to an agent for a particular run.

This does not mean recording everything the model internally computes. It means preserving the external engineering conditions that the organization supplied and can govern.

---

## Why Chat History Is Not an Engineering Record

A conversation transcript is useful, but it was designed to support interaction, not to serve as a complete execution record.

The transcript may show what a person typed and what an agent replied. It may not show every system instruction, retrieved artifact, tool definition, permission, context transformation, or file version involved in producing the reply.

Even when all messages remain available, the transcript leaves a harder question unanswered:

> Which parts of the available information formed the effective context of this specific action?

There are at least three different states:

```text
Available context
    Information the system could have retrieved

Delivered context
    Information actually supplied to the agent or model

Claimed basis
    Information the agent says influenced its result
```

These states must not be treated as equivalent.

A file existing in the repository does not prove that the agent read it. A rule appearing in a system prompt does not prove that the implementation complied with it. An agent citing a requirement does not prove that the requirement was the true cause of its output.

Governance does not require pretending that these limitations disappear. It requires recording each claim at the level that can actually be supported.

An execution record may prove that a versioned instruction was delivered. A tool trace may prove that a file was read or a test command was executed. A review may determine whether the resulting change complied with the instruction. None of those records, on its own, reveals the model's private reasoning.

That boundary is important. Prompt and context governance should produce inspectable engineering evidence, not a fictional reconstruction of an AI's mind.

[[M_EBG_A_02-2.png]]

---

## What Current Engineering Practices Already Solve

The industry is not starting from nothing. Several current practices preserve part of the execution basis.

Git records versioned project artifacts and source changes. A team can recover the repository state associated with a commit and compare what changed.

Specification-Driven Development, or SDD, moves intended work out of an ephemeral prompt and into persistent artifacts. Current tools use different structures, but commonly produce some combination of requirements, design, plans, and implementation tasks. Kiro uses requirements, design, and task artifacts. GitHub Spec Kit uses specifications, plans, and tasks. OpenSpec represents changes through proposals, delta specifications, design, and tasks.

This is an important engineering move:

```text
Intent only in conversation
    -> session ends
    -> intent becomes difficult to recover

Intent in a versioned specification
    -> session ends
    -> recorded intent remains inspectable
```

[[M_EBG_A_02-1.png]]

Agent observability is also advancing. Emerging telemetry conventions can record model requests, input and output messages, agent identity and version, conversation identifiers, token usage, retrieval data, and tool calls. These records help reconstruct technical execution and correlate activity across a workflow.

But each practice preserves a different layer:

- Git preserves repository state and change history.
- SDD preserves a structured statement of intended change.
- Conversation history preserves visible interaction.
- Telemetry preserves selected runtime events.
- Tests and reviews preserve verification results.

The governance gap appears between those layers.

Git does not identify the complete context delivered to the agent. An SDD artifact does not prove which version entered a run. A transcript does not necessarily expose hidden instructions or context transformations. Telemetry may record a tool call without explaining which approved change scope authorized it. A passing test does not prove that every governing constraint was considered.

The problem is no longer simply that information is missing. It is that the surviving records are not consistently bound into one versioned execution basis.

---

## From Conversation to a Versioned Execution Basis

The payment retry request should not enter the workflow only as text in a chat box. It should become an identifiable Prompt Artifact connected to an explicit Context Manifest.

The Prompt Artifact records the requested outcome, constraints, acceptance conditions, author, approval state, and version. It is not necessarily a copy of every conversational sentence. It is the governed instruction for the run.

The Context Manifest identifies the external inputs and capabilities that formed the run's engineering conditions. Depending on risk, it can include:

```text
Execution ID
Prompt Artifact ID and version
Change Scope ID and version
Repository commit or workspace state
Specification and architecture artifact versions
Applicable instruction and policy versions
Files and retrieved sources delivered to context
Conversation or summary version
Agent and model version
Available tools and permissions
Environment identity
Context truncation or transformation events
Start time, end time, and integrity metadata
```

Large or sensitive content does not always need to be duplicated. The manifest can reference a controlled artifact by stable identifier, version, and integrity hash. Access rules and retention policies can determine who may inspect the content.

This creates a stronger relationship:

```text
Prompt Artifact
    defines the governed request

Context Manifest
    identifies the external execution conditions

Execution ID
    binds those conditions to actions and results
```

The result is not perfect reproducibility. Models, external services, and non-deterministic tools may still produce different outputs. The practical governance goal is **basis reproducibility**: the organization can recover the controlled inputs and conditions against which a run should be reviewed or repeated.

---

## Context Must Include the System and the Change

A versioned prompt can still be incomplete if it describes only the requested feature.

The payment retry change belongs to a larger system. Business rules define when another attempt is allowed. System design defines payment states and failure behavior. Architecture defines dependency and transaction boundaries. Security and operational rules may prohibit specific implementations.

A change-level specification is useful because it bounds the current task. It does not automatically represent the system as a whole.

This is where the later concepts in this series fit, without becoming the subject of this article:

- **VSS** makes the relevant system specification observable across PM/BA, system design, system architecture, and other engineering viewpoints.
- **Scope** identifies the bounded part of that system involved in the current change.
- **Version** fixes both the system state and change boundary at the relevant point in time.
- **TraceID or Execution ID** connects that basis to execution records and resulting evidence.

For prompt and context governance, their immediate role is simple: the Context Manifest must be able to identify both the versioned system basis and the versioned change scope supplied to the run.

Without the system basis, the agent may satisfy the local request while violating an unchanged constraint. Without the change scope, the agent may interpret the entire repository as available for modification. Without versions, a later reviewer may inspect today's documents instead of the documents that governed the run at that time.

---

## Recording Context Is Not the Same as Governing It

Once context becomes observable, governance can finally perform concrete work.

Before execution, controls can verify that required specification viewpoints are present, the Scope is approved, referenced versions exist, and the agent's permissions match the task.

During execution, monitoring can identify context truncation, unexpected retrieval, unauthorized file access, tool calls outside Scope, or a change in the model or instruction set.

After execution, reviewers can compare the delivered context with the actions taken, inspect test and review evidence, assess exceptions, and determine whether the result should be accepted.

Across many runs, the organization can identify recurring failures: architecture rules that are frequently omitted from context, prompts that produce excessive scope expansion, summaries that remove critical constraints, or approvals that occur after implementation has already begun.

That is where PDCA becomes possible:

```text
Plan
    Define required prompt, context, scope, and controls

Do
    Execute under an identified and versioned basis

Check
    Compare actions and results with that basis

Act
    Correct the workflow, controls, specifications, or context assembly
```

Governance becomes repeatable because it no longer depends on someone remembering what the conversation meant.

[[M_EBG_A_02-3.png]]

---

## Engineering Comes Before the Governance Judgment

An organization may already have rules requiring authorized scope, architecture compliance, human approval, testing, traceability, or auditability.

Those governance requirements can exist on paper and still be impossible to apply to a concrete AI development run.

If the prompt is transient, the governed request cannot be recovered reliably. If the context is invisible, the applicable execution conditions cannot be established. If inputs have no versions, the past state cannot be reconstructed. If the execution has no stable identity, actions and evidence cannot be bound back to that state.

The first step is therefore not to add another governance principle. It is to engineer the object that governance needs to observe.

```text
Prompt
    from transient instruction to versioned Prompt Artifact

Context
    from implicit model input to identifiable Context Manifest

Execution
    from isolated conversation to traceable engineering run

Governance
    from general policy to repeatable control, review, and improvement
```

SDD helps by preventing intended work from disappearing with the conversation. Git helps preserve versions of the artifacts that exist. VSS and Scope can identify the relevant system state and bounded change. Execution identity can connect that basis to what happened next.

But this progression exposes a further problem.

Even when a run is traceable, not every retained record proves the same thing. A prompt, context manifest, tool trace, Git commit, test result, approval, and token report each support different governance claims.

The next question is therefore not simply whether the organization has evidence.

It is:

> What kind of evidence supports which engineering governance problem, and what can that evidence actually prove?

That is where traceability must become Engineering Decision Behavior Evidence.

---

## References

- [Kiro: Specs](https://kiro.dev/docs/specs/)
- [Kiro: Feature Spec best practices](https://kiro.dev/docs/specs/best-practices/)
- [GitHub Spec Kit](https://github.github.com/spec-kit/)
- [GitHub Spec Kit: Spec persistence models](https://github.com/github/spec-kit/blob/main/docs/concepts/spec-persistence.md)
- [OpenSpec: Spec-driven schema](https://openspec.dev/docs/schemas/spec-driven)
- [OpenSpec: Quickstart and archive model](https://openspec.dev/docs/quickstart)
- [OpenTelemetry: Generative AI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
