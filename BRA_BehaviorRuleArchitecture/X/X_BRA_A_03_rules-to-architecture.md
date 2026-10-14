# When Does a Collection of AI Rules Become an Architecture?

**Behavior Rule Architecture — Main Series 03 / 06**

[[X_BRA_A_03-0.png]]

Defining one Rule is a language problem. Managing many reusable Rules creates an architectural problem.

Each Rule needs an identity. Changes need versions. Teams need ownership and lifecycle state. Tools need a consistent structure. Projects need to find, select, and combine Rules without silently changing their meaning.

A collection becomes an architecture when those boundaries and relationships are designed explicitly.

## Separate the behavioral core from governance

The normative statement is the Rule’s stable behavioral core. Other information explains how the Rule is managed:

```text
Rule
├── Execution
│   ├── ID
│   ├── Apply As
│   └── Normative
└── Governance
    ├── Version
    ├── Status
    ├── Owner
    ├── Intent
    ├── Applicability Context
    └── Governance Impact
```

The important decision is not the exact field list. It is the separation.

Future governance may require evidence, risk, exceptions, provenance, effectiveness, or supersession. Those concerns should be able to evolve without silently redefining the Rule’s normative meaning.

## Make structure validatable, not arbitrary

Human-readable Rule documents can drift. One uses `Version`, another `Revision`; one has an owner, another omits it. Humans may compensate, but software cannot depend on inconsistent conventions.

BRA uses YAML as a reference representation and a schema to define a stable structural boundary with bounded extensibility.

Validation can answer:

> Is this a structurally and semantically usable Rule artifact?

It cannot answer:

> Is this AI action allowed at runtime?

A machine-valid Rule is not a runtime enforcement system.

## Move dynamic context outside the atomic Rule

If every combination of action, target, context, and stage becomes another Rule, reuse collapses into duplication.

The atomic Rule should remain as stable and portable as possible. Task-specific selection and dynamic boundary binding belong outside it.

That makes classification useful. Categories such as Artifact Isolation, Boundary, Traceability, Structural Change, or Test Integrity help people find Rules. A recognizable ID can carry a classification signal without becoming the whole classification system.

## Compose without rewriting

A **Rule Library** provides an authoritative, version-controlled source for reusable Rule assets.

A development task rarely needs the whole Library, so a **Ruleset** selects the relevant Rules.

The composition boundary is critical:

1. Categories organize Rules; they do not compose behavior.
2. Application Rulesets select and combine Rules.
3. Rules remain atomic and independent.

```text
Rule        -> one normative constraint
Rule Library -> reusable source of truth
Ruleset      -> contextual selection and composition
External System -> actual consumption or enforcement
```

BRA emerged from AI-assisted software development. It does not, by itself, establish a complete architecture for deployed autonomous or safety-critical behavior.

Its central principle is narrower and practical: **keep each Rule small enough to remain stable while keeping the surrounding architecture extensible enough to evolve.**

## Architecture should reduce coupling

Adding schemas, IDs, and directories is not sufficient if every change still propagates through the whole system.

A useful boundary can be tested with change scenarios. If ownership metadata changes, must the normative text change? If a project selects another Ruleset, do the underlying Rules acquire new meanings? If a Skill is replaced, does the Rule Library remain usable? If one Rule is revised, can historical decisions still resolve the old version?

When the answer is yes, the architecture separates responsibilities. When every answer requires editing copied instructions across projects and tools, the system still behaves like a collection of prompt fragments.

Architecture is therefore visible not in the number of artifacts, but in which concerns can evolve independently while their relationships remain traceable.

In your current rule collection, which responsibilities belong to the Rule—and which should belong to the Library, Ruleset, or consuming system?

#BehaviorRuleArchitecture #SoftwareArchitecture #AIGovernance #SoftwareEngineering
