# When Does a Collection of Rules Become an Architecture?

*From an atomic Rule to schema, governance, classification, and composition*

**Behavior Rule Architecture | 03 / 06**

In Part 02, I asked a basic question:

> **What exactly is a Rule?**

That question gradually led from natural-language instructions to constrained normative expressions, and eventually to an atomic behavioral Rule.

But once a Rule became reusable, a different class of problems appeared.

How do I identify it?

What happens when it changes?

What information belongs to the Rule itself?

What information might governance need later?

What happens when the number of Rules starts growing?

And how do multiple Rules work together without changing each other's meaning?

At that point, I was no longer only defining a Rule.

I was beginning to design an architecture.

Looking back, I can trace this transition to **March 2026**, when the work on Rules, Constraints, and Rulesets began to converge into what I would call Behavior Rule Architecture. As these artifacts became structured and reusable, I had to determine how they could be identified, governed, classified, and composed without silently changing their behavioral meaning.

Each structural decision solved one immediate management problem, but the underlying issue remained: a collection of valid Rules did not automatically define how those Rules should coexist as engineering artifacts.

At the time, I was no longer only refining instruction language. I was defining the boundaries between language, Rule, governance assets, and external execution.

Before going further, however, one boundary is important.

**BRA originated in AI-assisted software development.**

The behaviors I was trying to constrain were primarily behaviors involved in creating and modifying software-development artifacts:

```text
AI-Assisted Software Development
├── Generate / modify documents
├── Generate / modify source code
└── Generate / modify tests
```

The problem was not originally:

> How should every kind of AI behavior be governed?

It was much narrower:

> **How can I express and manage Rules that constrain AI behavior while it participates in software-development work?**

The architecture later became increasingly abstract and reusable, but that should not be confused with evidence of universal applicability.

In particular, this work did **not** establish that BRA is sufficient for governing:

- deployed AI runtime behavior,
- autonomous agent actions,
- physical or cyber-physical actions,
- operational decision execution,
- or other AI behaviors outside the development context.

Those domains may eventually reuse parts of the architecture, but they introduce different execution, authority, state, safety, and enforcement problems.

This article therefore describes BRA from the domain in which it emerged:

> **AI behavior during software development.**

---

## Problem 1: A Rule could be defined, but how should it exist as a manageable object?

A normative statement might already be understandable:

> AI MUST NOT modify test code when fixing source code unless test modification is explicitly authorized.

But once I wanted to reuse that Rule, the sentence itself was not enough.

I needed to reference it.

So it needed an **ID**.

Then the Rule changed.

So it needed a **Version**.

Then more questions appeared:

Who owns it?

Is it active or deprecated?

Why does it exist?

Who is responsible for it?

In what context is it relevant?

What impact or evidence might governance eventually care about?

I could keep adding fields forever.

That exposed a more important design problem:

> **I did not need to predict every property a Rule might ever need. I needed to separate what must remain stable from what could evolve.**

This led to a much simpler abstraction:

```text
Rule
├── Execution
│   ├── ID
│   ├── Apply As
│   └── Normative
│
└── Governance
    ├── Version
    ├── Status
    ├── Owner
    ├── Intent
    ├── Responsibilities
    ├── Applicability Context
    ├── Governance Impact
    └── ...
```

The important part was not the individual fields.

It was the separation.

The **Normative** remained the behavioral core.

The other information described how that Rule could be understood, managed, traced, reviewed, and eventually governed.

That meant adding a future governance concern did not necessarily require redefining the behavioral meaning of the Rule.

---

## Problem 2: I could not know every governance requirement in advance

This became one of the most important design decisions.

I could define the governance information I needed at that moment:

```text
Version
Status
Owner
Intent
Responsibilities
Applicability Context
Governance Impact
```

But there was no reason to assume this list was complete.

A future governance process might care about:

```text
Evidence
Authority
Risk
Review Result
Effectiveness
Provenance
Exception
Supersession
...
```

Trying to predict every future governance requirement would make the Rule increasingly complex.

Worse, if every new governance concern changed the Rule's normative structure, the behavioral artifact itself would never stabilize.

So I deliberately kept **Governance highly abstracted**.

Conceptually:

```text
Stable Behavioral Core
          │
          ▼
        Rule
          │
          ▼
Abstract Governance Surface
          │
          ├── Current governance needs
          ├── Future governance needs
          ├── Audit information
          ├── Evidence expectations
          └── Lifecycle information
```

The principle was:

> **Normative defines behavior. Governance provides a place for governance information to evolve without silently redefining that behavior.**

This abstraction was intentional.

I did not know what every future governance system would require.

I did know that future governance should not force me to continually redesign the normative core.

This also left room for something that became increasingly important later:

> **Lifecycle and PDCA.**

A Rule itself does not perform PDCA.

It does not define a governance workflow.

But governance information can preserve enough state for an external process to eventually do something like:

```text
Plan
→ Define / revise the Rule

Do
→ Apply the Rule

Check
→ Review results / evidence

Act
→ Adjust the Rule

↓
New Version
↓
Repeat
```

That distinction mattered.

```text
Rule
→ What behavioral constraint exists?

Governance
→ What governance information can be attached?

Governance System
→ What should be done with that information?
```

I did not need to build the entire governance system into the Rule.

I needed to avoid designing the Rule in a way that would prevent governance from evolving later.

---

## Problem 3: If the structure could evolve, how could it remain consistent?

Once a Rule contained structured information, another practical problem appeared.

I could represent it in Markdown.

Markdown was easy to read and easy to maintain in Git.

But conventions could gradually diverge.

One Rule might use:

```text
Version
```

another:

```text
Revision
```

another:

```text
Ver
```

One might contain an Owner.

Another might forget it.

One team might represent Intent as text.

Another might invent a completely different structure.

Humans could usually understand the documents.

Software could not reliably depend on them.

So the question changed from:

> Can humans read this Rule?

to:

> **Can a system recognize whether this artifact has the structure a Rule is supposed to have?**

That required a structured representation.

I chose **YAML as a reference representation**.

Not because BRA itself had to be YAML.

The Rule concept remained representation-agnostic.

YAML was useful because it was both human-readable and machine-readable.

For example:

```yaml
execution:
  id: CODE-TI-01
  apply_as: qa
  normative: >
    AI MUST NOT modify test code when fixing source code
    unless test modification is explicitly authorized.

governance:
  version: "1.0.0"
  status: active
  owner: engineering

  intent:
    rationale:
      - preserve_test_independence
```

Once the representation became structured, I could define something else:

> **Schema.**

And once a Schema existed:

```text
Rule
↓
YAML Reference Representation
↓
Rule Schema
↓
Validation
↓
Valid / Invalid
```

Now structure could be checked.

Missing ID?

Invalid.

Missing required governance information?

Invalid.

Wrong structure?

Invalid.

Unexpected top-level properties?

Invalid.

At the same time, selected governance areas could still support organization-defined attributes.

That gave me something I needed on both sides:

> **A stable structural boundary with bounded extensibility.**

The architecture could evolve without becoming structurally arbitrary.

And validation still had a clear boundary.

[[M_BRA_A_03-0.png]]

It could answer:

> Is this a structurally and semantically usable Rule artifact?

It did **not** answer:

> Should this action be allowed at runtime?

That was a different problem.

This distinction becomes especially important when discussing BRA outside software development.

A Rule schema being machine-validatable does not make it a runtime enforcement architecture.

---

## Problem 4: Why was the number of Rules growing so quickly?

Once individual Rules became manageable, I ran into a problem outside the Rule itself.

There were too many of them.

Part 02 had already exposed **Action** and **Target** as useful dimensions.

For example:

```text
modify × source_code
modify × test_code
modify × document
```

But if every combination became another Rule, the number of Rules would grow quickly.

Add more Actions:

```text
create
modify
delete
refactor
```

and more Targets:

```text
source_code
test_code
document
config
schema
script
```

and the Rule collection begins to look like:

```text
Action × Target × Context × Stage
```

That was not scalable.

The same behavioral principle was being repeated only because the development context had changed.

So I started separating two questions:

```text
What behavioral constraint exists?
→ Rule

Where should that Rule be selected or applied?
→ External context / selection
```

For example:

```text
Source-code generation
├── modify + source_code → relevant
└── modify + test_code   → restricted

Test maintenance
└── modify + test_code   → relevant
```

This significantly changed how I thought about Rules.

The Rule should remain as atomic and reusable as possible.

Development-task-specific scope should not be repeatedly hard-coded into otherwise identical Rules.

This also explains an architectural decision that became explicit later:

> **Boundary declaration should not be part of the atomic Rule itself.**

Dynamic scope binding belongs outside the Rule.

That keeps the Rule portable across different development tasks, tools, and workflows.

So Part 02 had discovered:

```text
Action × Target
```

Part 03 exposed the next problem:

> **If every Action × Target combination becomes another Rule, reuse collapses into duplication.**

The solution was not to write Rules faster.

It was to abstract them better.

---

## Problem 5: Fewer Rules still did not mean Rules were easy to find

Reducing duplicated Rules helped.

But a reusable Rule Library could still contain dozens or hundreds of Rules.

Then another problem appeared:

> **How do I recognize what a Rule is about?**

That led to **Classification**.

In the development Rule Library, recurring concerns began forming categories such as:

```text
AR — Artifact Isolation
BD — Boundary & Stop
CN — Constraint Neutrality
TR — Traceability
LG — Logging & Report
ST — Structural Change
TI — Test Integrity
```

Classification was also reflected in Rule identity.

For example:

```text
CODE-TI-01
CODE-BD-01
CODE-TR-01
```

The ID was no longer only a unique identifier.

It also carried a human-recognizable classification signal.

That meant even if a Rule was copied into another context or shown outside its original directory, its identity still provided some indication of where it belonged.

This did not make the ID the entire classification system.

But it made classification visible at the point of reference.

---

## Problem 6: Classified Rules were still scattered Rules

Classification made Rules easier to recognize.

It did not solve reuse.

If every project kept its own copy:

```text
Project A
└── CODE-TI-01 v1.0

Project B
└── CODE-TI-01 modified copy

Project C
└── CODE-TI-01 older copy
```

then the same Rule could quietly become several different Rules.

So Rules needed a reusable source of truth.

That led to the:

> **Rule Library**

Conceptually:

```text
Rule Library
├── AR
├── BD
├── CN
├── TR
├── LG
├── ST
└── TI
```

Now the unit of reuse was no longer the prompt or the project document.

It was the Rule artifact itself.

But centralizing Rules created another problem.

A development task rarely needs every Rule in the Library.

---

## Problem 7: How could I use multiple Rules without turning them into another giant Rule?

A particular development context needs a selection.

For example:

```text
Source Generation
↓
Traceability Rules
+
Artifact Isolation Rules
+
Boundary Rules
+
Test Integrity Rules
```

That led to **Ruleset**.

But I needed to preserve one principle:

> Combining Rules must not silently rewrite the individual Rules.

A Rule should not acquire different behavioral meaning simply because it appears beside another Rule.

That led to a distinction between two forms of grouping.

A **Category Ruleset** organizes related Rules:

```text
Test Integrity
├── Rule 01
├── Rule 02
└── Rule 03
```

An **Application Ruleset** selects Rules for a particular use:

```text
Application Ruleset
├── AR-...
├── BD-...
├── TI-...
└── TR-...
```

And this eventually produced several composition principles:

1. **Category MUST NOT define Rule composition.**
2. **Rule composition MUST occur only in Application Ruleset.**
3. **Rules MUST remain atomic and independent.**

This preserved an important architectural boundary:

```text
Rule
→ defines one atomic normative constraint

Rule Library
→ manages reusable Rule assets

Ruleset
→ selects and composes Rules

External System
→ determines how those Rules are actually used
```

The Rule itself did not need to know which Ruleset contained it.

That independence was what made reuse possible.

---

## At some point, this was no longer just a Rule format

Looking back, the progression was not:

> I decided to design Behavior Rule Architecture.

It was closer to this:

```text
AI-assisted software-development behavior
↓
What is a Rule?
↓
Atomic Normative Rule

How should a Rule exist?
↓
Execution + Governance

How can governance evolve without redefining behavior?
↓
Abstract Governance Surface

How can the structure remain consistent?
↓
Structured Representation
↓
YAML
↓
Schema
↓
Validation

Why are there so many Rules?
↓
Separate reusable Rule from development-specific context

How can I recognize Rules?
↓
Classification
↓
Classification reflected in ID

How can Rules be reused?
↓
Rule Library

How can different development contexts use different combinations?
↓
Ruleset

How can composition avoid changing individual Rules?
↓
Composition Principles

↓

Behavior Rule Architecture
```

The architecture did not come from adding more fields.

In several places, the opposite happened.

The architecture emerged by deciding:

- what must stay inside the Rule,
- what must remain descriptive,
- what should be extensible,
- what should move outside the Rule,
- and what should be managed at a higher level.

That distinction became more important than any individual schema field.

[[M_BRA_A_03-1.png]]

---

## Behavior Rule Architecture

By this point, the system had several different architectural objects:

```text
Atomic Rule
│
├── Stable normative core
├── Abstract governance surface
└── Structured representation
        │
        ▼
      Schema
        │
        ▼
    Validation

Rules
│
├── Classification
│
└── Rule Library
        │
        ▼
      Ruleset
        │
        ▼
Composition Principles
```

Together, these became what I called:

> **Behavior Rule Architecture — BRA**

But the name needs a boundary.

BRA emerged as an architecture for representing and organizing behavioral Rules for **AI participating in software-development activities**.

Its original problem space included behaviors such as:

```text
Document work
→ create / modify development documents

Code work
→ create / modify source code

Test work
→ create / modify tests
→ perform development-stage testing activities
```

Within that scope, BRA treats behavioral Rules as reusable engineering artifacts while separating their normative meaning, governance information, lifecycle potential, classification, and composition.

It does **not**, by itself, establish a general architecture for every form of AI behavior.

In particular:

```text
BRA demonstrated / designed scope
→ AI-assisted software-development behavior

Not established by this work
→ deployed AI runtime behavior
→ autonomous operational actions
→ physical actions
→ safety-critical control actions
→ general agent execution governance
```

This is not a claim that BRA could never be extended to those domains.

It is a claim about architectural evidence:

> **Abstraction is not the same as validated applicability.**

A Rule representation may be sufficiently abstract to travel into another domain.

That does not mean the surrounding assumptions, boundary model, enforcement requirements, authority model, or safety controls automatically travel with it.

For BRA, the original engineering domain remains important.

And one principle became increasingly clear:

> **A Rule should remain small enough to stay stable, while the architecture around it remains extensible enough to evolve.**

---

## Why I am publishing the BRA repository here

Parts 01 and 02 could mostly be explained as a sequence of ideas.

Part 03 introduces something different:

> an architecture and its schema.

At this point, an article is no longer the best place to show the complete structure.

So I am publishing the public BRA repository together with this part of the series.

This article explains:

> **Why did each architectural element emerge?**

The repository provides the reference for:

> **What does the architecture actually look like?**

It includes the Rule model, schemas, classifications, Rule Library structure, Ruleset structure, examples, and architecture documentation.

**BRA Repository**

`[URL]`

---

## The next problem: architecture was no longer enough

Once Rules had:

```text
Identity
+
Structure
+
Schema
+
Validation Model
+
Classification
+
Library
+
Composition
```

a new class of questions appeared.

Who actually validates the Rule?

How do I inspect a Ruleset?

How does a coding agent consume these Rules?

How can the same Rule be adapted for different AI development tools?

How should validation results and evidence be recorded?

Those were no longer Rule-definition problems.

They were software infrastructure problems.

That is where LBRA moves next:

> **Part 04 — How Do You Actually Use a Behavior Rule Architecture?**



