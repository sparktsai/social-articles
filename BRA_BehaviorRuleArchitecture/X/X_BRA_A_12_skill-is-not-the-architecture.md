# Your AI Skill Should Consume the Rule Architecture—not Become It

**Behavior Rule Architecture — Problem Deep Dive 06 / 08**

[[X_BRA_A_12-0.png]]

A Skill selects Rules, prepares context, and guides an AI coding workflow. It works well, so the team starts treating the Skill as the Rule system itself.

That creates tool lock-in at the wrong architectural layer.

Rules should survive changes in Skills, coding agents, IDEs, CLIs, and model providers. The consumer depends on the Rule infrastructure—not the reverse.

## Separate five responsibilities

Behavior Rule Architecture defines how Rules are represented and organized.

The Rule Library provides an authoritative, version-controlled home for those assets.

A Validator controls the quality of Rules entering the Library.

A Skill resolves applicable Rules and prepares an execution view inside an AI workflow.

A CLI exposes inspection, validation, retrieval, or resolution to humans, scripts, and CI.

```text
BRA -> representation and organization
Library -> persistence and versioned truth
Validator -> controlled write path
Skill -> workflow consumption
CLI -> alternative access path
```

Combining these responsibilities in one Skill may be convenient initially. It makes future changes harder to reason about.

## The dependency direction matters

A healthy dependency looks like:

```text
BRA
  -> Rule Library
     -> Skill
     -> CLI
     -> CI
     -> another development tool
```

The Rule does not need to know which Skill consumes it. The Library does not need to be specific to one coding assistant. A CLI does not need to understand the full development workflow.

Each consumer asks the same infrastructure for the representation it needs.

## A Skill can automate selection without owning meaning

At task start, a Skill may identify the development scenario, resolve an Application Ruleset, retrieve current Rule versions, create a minimal execution view, and record delivery.

Those are meaningful orchestration responsibilities.

But the Skill should not become the only place where normative text, ownership, or version history exists. Otherwise replacing the Skill also replaces the Rule system.

The same applies to model-specific instruction files. They may provide an adapter or entrypoint, but reusable behavioral meaning should remain upstream.

## Keep write and read paths distinct

Creating or revising a Rule should go through validation and review before entering the Library.

Consuming a Rule should resolve an accepted version without silently modifying it.

```text
Write: Author -> Validate -> Review -> Rule Library
Read: Task -> Resolve -> Project View -> Model
```

This boundary prevents workflow convenience from becoming an uncontrolled Rule-authoring path.

It also lets the organization replace a Skill, add a CLI, or support another agent without migrating the normative assets themselves.

## Consumer independence has a limit

Different tools may require different adapters, formats, or delivery mechanisms. Portability does not mean pretending every consumer behaves identically.

The stable contract should be the Rule identity, version, normative meaning, and resolution semantics. A consumer-specific layer can translate those assets into the format a model or tool can use, while recording any truncation, transformation, or unsupported capability.

If a tool cannot preserve a necessary condition, the system should expose that limitation rather than silently weakening the Rule. This allows the Library to remain independent without hiding meaningful differences between consumers.

Architecture-level portability is achieved through explicit adapters and evidence—not by assuming one instruction file works everywhere.

The same principle protects the architecture from vendor-specific terminology. Tool features can be mapped at the adapter boundary without renaming the governed Rule every time the toolchain changes.

The practical test is portability: if your current AI Skill disappeared tomorrow, would the Rules, versions, ownership, and composition model still exist as usable engineering assets?

## Source

- [Contract Coding Skill](https://github.com/NextEvoEco/contract-coding-skill)

#BehaviorRuleArchitecture #AISkills #DeveloperTools #SoftwareArchitecture
