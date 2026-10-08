# Putting AI Rules to Work

> Deliver the right rules through libraries, skills, and CLI tools during development.

In the previous parts of this series, the problem gradually changed.

First, I moved repeated behavioral instructions out of individual prompts.

Then I asked what a Rule actually was.

Then Rules became structured artifacts with identity, normative meaning, governance information, classification, Rulesets, and a Rule Library.

That eventually became **Behavior Rule Architecture — BRA**.

But an architecture creates another question:

> **How do you actually use it?**

For me, this was not initially an infrastructure problem.

It was a very practical software-development problem.

I was using AI to work with different development artifacts:

- requirements and specification documents,
- source code,
- test code,
- and other development artifacts.

Different tasks required different behavioral constraints.

The question was simply:

> **How do I give the AI the right Rules for the development task I am performing right now?**

That question changed the way I used BRA several times.

---

## I had Rulesets, but how did I actually apply them?

This was before Skills became a common way to package AI development workflows.

My early usage was much simpler.

When working with VS Code Copilot, I specified the relevant Ruleset in the prompt according to the development scenario.

Conceptually:

```text id="q04-01"
Modify Requirement Document
→ Apply the relevant specification Ruleset

Generate Source Code
→ Apply the relevant code Ruleset

Generate / Modify Tests
→ Apply the relevant test-related Ruleset
```

The usage model looked like this:

```text id="q04-02"
Development Task
↓
Identify Current Scenario
↓
Select Matching Ruleset
↓
Provide Rules to the LLM
↓
Perform Task
```

This worked.

And it demonstrated something useful about Rulesets.

I did not need every Rule for every task.

The Rules required for modifying a specification were not necessarily the same Rules required for generating source code or working with tests.

The **development scenario determined which Ruleset should be applied**.

That was much better than maintaining one enormous universal prompt.

But once I started using the Rules this way, I encountered another problem.

The Rules themselves had become too rich.

---

## A complete Rule was useful for governance, but too heavy for every inference

By this point, a Rule was no longer just one normative sentence.

A complete Rule could contain information such as:

```text id="q04-03"
Rule
├── ID
├── Version
├── Normative Expression
└── Governance
    ├── Status
    ├── Owner
    ├── Intent
    ├── Responsibilities
    ├── Applicability Context
    ├── Governance Impact
    └── ...
```

This information existed for a reason.

If Rules were going to become reusable engineering artifacts, I wanted to know things such as:

Who owns this Rule?

Why does it exist?

Which version is current?

What governance context surrounds it?

What should be reviewed later?

That information was valuable for management, traceability, governance, and future lifecycle processes.

But it created a different problem when I passed the complete Rule to an LLM.

The LLM did not necessarily need all of that information to perform the immediate development task.

If the task was:

> Generate source code under these behavioral constraints.

then the model primarily needed the behavioral constraints.

Giving it every governance field had two costs.

First, it introduced additional semantic material into the inference context.

Second, context windows at the time were much more constrained than they are today.

A Ruleset containing many complete Rules could therefore consume a significant amount of context before the actual requirement, specification, source code, or test context was even included.

This exposed an important distinction:

> **The complete Rule artifact and the Rule representation needed for one execution did not have to be identical.**

I still wanted the complete Rule.

I just did not need to send all of it to the LLM every time.

---

## I needed one representation for governance and another for execution

My response was to separate the two concerns.

I created a repository that could preserve the complete Rule system.

Conceptually:

```text id="q04-04"
Rule Repository
│
├── NNL
├── CNL
├── Rules
├── Rulesets
├── Governance Information
└── Version History
```

The repository preserved the complete artifacts.

It could be version controlled.

Changes could be reviewed.

Rules could evolve without losing their history.

Governance information remained attached to the engineering assets that required it.

This repository became the authoritative source.

But I did not send all of that content to the LLM.

For actual development tasks, I created smaller scenario-specific files.

For example:

```text id="q04-05"
requirement-update.rules
source-generation.rules
test-generation.rules
```

Instead of carrying the complete Rule, each execution-facing Rule could be reduced to something much smaller:

```text id="q04-06"
ID
Version
CNL
```

Conceptually:

```yaml id="q04-07"
- id: CODE-TI-01
  version: "1.0.0"
  cnl: >
    AI MUST NOT modify test code
    unless the task explicitly authorizes it.
```

The relationship became:

```text id="q04-08"
Complete Rule
│
├── ID
├── Version
├── CNL
├── Intent
├── Owner
├── Responsibilities
├── Applicability Context
├── Governance Impact
└── ...

          ↓ projection

Execution View
│
├── ID
├── Version
└── CNL
```

This was an important change in how I thought about BRA.

I no longer assumed that one artifact representation had to satisfy every consumer.

The complete Rule was useful for engineering management and governance.

The compact Rule was useful for LLM execution.

They represented the same Rule for different purposes.

In other words:

> **Governance information could be preserved without requiring all governance information to participate in every LLM inference.**

[[M_BRA_A_04-0.png]]

This also changed the role of the repository.

It was no longer merely a place where I stored some Rule files.

It was becoming **Rule infrastructure**.

---

## The Rule Library became the infrastructure

This distinction matters.

BRA defines how behavioral Rules can be represented and organized.

The **Rule Library** gives those Rules a persistent, shared, version-controlled place to exist.

Conceptually:

```text id="q04-09"
BRA
↓
Rule Library
↓
Development Workflows
↓
Projects
```

The Rule Library could become a common dependency rather than something copied independently into every project.

That meant the Rule itself could have one authoritative engineering representation while different downstream workflows consumed only what they needed.

This was already useful.

But separating the authoritative Rule from its compact execution representation created another problem.

---

## Two representations created a synchronization problem

Suppose the Rule Library contained:

```text id="q04-10"
CODE-TI-01
Version 1.2
```

but a scenario-specific execution file still contained:

```text id="q04-11"
CODE-TI-01
Version 1.1
```

Now I had two questions:

> Which Rule was current?

and, more importantly:

> **Which version did the AI actually receive?**

The architecture might have one authoritative version while the development workflow was still using an older copy.

The flow looked like this:

```text id="q04-12"
Rule Library
     │
     │ manual projection / copy
     ▼
Scenario Rules File
     │
     ▼
Prompt
     │
     ▼
LLM
```

In practice, Rules did not change constantly.

Once a Rule became stable, updates might only happen occasionally.

So this was not necessarily a frequent operational failure.

But architecturally the dependency still existed.

> **Low update frequency reduces synchronization failures. It does not eliminate synchronization dependency.**

The moment I maintained both an authoritative Rule and a separately stored execution copy, version drift became possible.

That raised a better question:

> Why should I store the execution copy at all?

---

## If Rules were engineering assets, how should new Rules enter the Library?

There was also another side to the Rule Library.

So far I had mostly been thinking about how to **read** Rules.

But Rules also had to be created and changed.

If someone wrote:

```text id="q04-13"
AI should probably avoid changing unrelated files.
```

was that already a valid Rule?

Not necessarily.

It might still contain ambiguous normative language.

Its structure might be incomplete.

Required attributes might be missing.

Its normative statement might not conform to the Rule representation.

So the Rule Library needed a controlled write path.

That led to **Rule validation**.

Conceptually:

```text id="q04-14"
Create / Modify Rule
↓
Validate Structure
↓
Validate Normative Expression
↓
Check Ambiguity / Usability
↓
Accept or Revise
↓
Rule Library
```

The important boundary was:

> **The Validator validates the Rule artifact. It does not enforce the Rule against AI behavior.**

These are very different questions.

The Validator asks:

> Is this Rule structurally and semantically acceptable as a behavioral constraint artifact?

It does not ask:

> Is the AI currently allowed to perform this action?

And it does not prove:

> Did the AI actually follow this Rule?

Those problems belong elsewhere.

This gave the Rule Library two distinct paths:

```text id="q04-15"
WRITE PATH

Human / AI
↓
Create or Modify Rule
↓
Validator
↓
Rule Library


READ PATH

Development Task
↓
Select Rules
↓
Provide Execution View
↓
LLM
```

The write path was becoming manageable.

The read path still had the synchronization problem.

---

## Skills changed when the execution view could be created

The next major change came when Skills became practical as a way to package AI development workflows.

This changed the problem significantly.

Previously, I prepared the compact execution representation in advance:

```text id="q04-16"
Rule Library
↓
Prepare Compact Ruleset
↓
Store Compact Ruleset
↓
Prompt
↓
LLM
```

But if a pre-processing Skill could access the Rule Library when the task started, I no longer needed to maintain that intermediate copy manually.

The workflow could instead become:

```text id="q04-17"
Development Task
↓
Pre-process Skill
↓
Identify Current Scenario
↓
Access Rule Library
↓
Resolve Current Ruleset
↓
Retrieve Latest Rule Versions
↓
Build Minimal Execution View
↓
Continue Development Task
```

This changed the Rule delivery model.

Before:

> **Store an execution copy.**

After:

> **Resolve the execution view when it is needed.**

That is a small implementation change with a significant architectural consequence.

The authoritative Rule can remain in the Rule Library.

Governance information can remain there.

Version history can remain there.

The LLM can still receive a small execution-facing representation.

But that representation no longer has to become another independently maintained source of truth.

Conceptually:

```text id="q04-18"
                 Rule Library
                      │
             authoritative Rule
                      │
                      ▼
              Pre-process Skill
                      │
              resolve at use time
                      │
                      ▼
              Execution View
              ID + Version + CNL
                      │
                      ▼
                    LLM
```

This is much closer to what I originally wanted.

One governed Rule.

Different usage contexts.

Minimal information sent to the model.

No need to treat every execution representation as another Rule artifact that must be maintained separately.

---

## From prompt selection to Contract Coding Skill

This pattern eventually became part of a broader AI-assisted development workflow.

Instead of manually remembering which Rules to insert into every development prompt, the workflow could perform pre-processing before the main development action.

For example:

```text id="q04-19"
Current Development Intent
↓
Determine Development Stage / Task
↓
Resolve Applicable Rules
↓
Prepare Execution Context
↓
Generate / Modify Artifact
```

This idea later became part of my **Contract Coding Skill** work.

The implementation is available here:

**Contract Coding Skill**

https://github.com/NextEvoEco/contract-coding-skill

The important point is not that BRA was originally designed for Skills.

It was not.

The historical order was the opposite:

```text id="q04-20"
Rules
↓
Rulesets
↓
Prompt-based Selection
↓
Context Problem
↓
Rule Repository
+
Compact Execution Files
↓
Synchronization Problem
↓
Pre-process Skill
↓
Resolve Latest Rules at Use Time
↓
Contract Coding Skill
```

The Skill was a later consumption mechanism for an architecture that already existed.

---

## A Skill should not become the architecture

Once the Skill worked, another distinction became important.

It would have been easy to start treating:

> BRA = Skill.

But that would repeat an earlier mistake.

A Rule should not belong to a prompt.

A Rule should not belong to VS Code Copilot.

And a Rule should not belong to one Skill implementation either.

The dependency should run in the opposite direction:

```text id="q04-21"
BRA
↓
Rule Library
↓
Consumer
├── Skill
├── CLI
└── Other Development Tool
↓
Project
```

The **Rule Library is the infrastructure**.

The Skill is one way of consuming it.

That also means I can provide another access mechanism without redesigning BRA.

One obvious example is a CLI.

---

## CLI: another way to consume the same Rule infrastructure

A Skill is useful when an AI development workflow needs to resolve Rules automatically.

But not every consumer has to be an AI Skill.

A developer may want to inspect a Rule.

A CI process may want to validate a Rule artifact.

A script may need the current version of a Ruleset.

A project setup process may need to retrieve a specific Rule.

Those are natural CLI operations.

Conceptually:

```text id="q04-22"
               Rule Library
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
        Skill                CLI
          │                   │
          ▼                   ▼
AI Development           Human / Script /
Workflow                 CI / Tooling
```

Possible operations are straightforward:

```text id="q04-23"
bra validate
bra inspect
bra get
bra resolve
```

The CLI does not create another architecture.

It exposes another way to work with the same Rule infrastructure.

That distinction keeps the architecture independent of its delivery mechanism.

---

## The usage model had changed

Looking back, the evolution was not mainly about adding more sophisticated tools.

It was about progressively removing unnecessary duplication between the Rule and its use.

The first model was:

```text id="q04-24"
Rules live in or near the Prompt
↓
LLM
```

Then:

```text id="q04-25"
Full Rules live in Repository
+
Compact Rules live in Scenario Files
↓
Prompt
↓
LLM
```

And later:

```text id="q04-26"
Full Rules live in Rule Library
↓
Resolve Current Rules on Demand
↓
Minimal Execution View
↓
LLM
```

The progression can be summarized even more simply:

```text id="q04-27"
Copy Rules
↓
Reference Rules
↓
Resolve Rules
```

That was the practical evolution of how I used BRA.

---

## BRA was not the Skill

This also clarified several architectural boundaries.

```text id="q04-28"
BRA
→ defines how behavioral Rules are represented and organized

Rule Library
→ provides persistent, version-controlled Rule infrastructure

Validator
→ controls the quality of Rules entering that infrastructure

Skill
→ resolves and consumes Rules inside an AI development workflow

CLI
→ provides another way for humans and software to access the same infrastructure
```

This separation matters because every layer can evolve independently.

The Rule does not have to change because the Skill changes.

The Rule Library does not have to become specific to VS Code Copilot.

The CLI does not need to understand every development workflow.

And governance information does not have to be sent to the LLM merely because it needs to be preserved.

[[M_BRA_A_04-1.png]]

---

## The scope is still AI-assisted software development

The concrete usage described in this article came from software-development activities:

```text id="q04-29"
Requirements / Specifications
↓
Source Code
↓
Tests
↓
Other Development Artifacts
```

That is where these Rule-selection, context, repository, and Skill patterns were developed.

BRA may prove useful in other AI behavior domains.

This article does not establish or exclude that possibility.

Its evidence comes from AI-assisted software development.

> **The origin tells us where the current usage model came from. It does not necessarily define where the architecture must end.**

---

## But one problem was still unresolved

At this point, I could answer several questions.

Where is the authoritative Rule?

> In the Rule Library.

Which version should be used?

> Resolve the current version from the Library.

How does a development workflow obtain the relevant Rules?

> Through a Skill, CLI, or another consumer.

How do I keep governance information without filling every LLM context with it?

> Preserve the complete Rule and generate a smaller execution view.

How do I check a newly created Rule?

> Validate it before accepting it into the Library.

But there was still one question none of this answered.

Suppose the workflow selected:

```text id="q04-30"
CODE-TI-01
Version 1.2
```

Suppose the correct Rule reached the model.

Suppose the development task completed.

Then:

> **Did the AI actually follow the Rule?**

A Rule being stored does not prove that it was selected.

A Rule being selected does not prove that it influenced the decision.

A Rule being included in context does not prove that the resulting behavior complied with it.

And even if the AI followed the Rule, another question remains:

> **Was the Rule actually effective?**

That requires something different.

Not another Rule format.

Not another Ruleset.

Not another delivery mechanism.

It requires **evidence**.

And once evidence exists, it can feed something that the Governance structure was designed to leave room for from the beginning:

```text id="q04-31"
Define Rule
↓
Apply Rule
↓
Observe Behavior
↓
Collect Evidence
↓
Evaluate
↓
Keep / Revise / Supersede Rule
↓
New Version
↺
```

That is where the next part begins:

> **Part 05 — How Do You Know the AI Actually Followed the Rule?**

From behavioral Rules to decision evidence, evaluation, and PDCA.

Behavior Rule Architecture · 04 / 06

#ArtificialIntelligence #AIGovernance #SoftwareEngineering #AIAgents #DeveloperTools



