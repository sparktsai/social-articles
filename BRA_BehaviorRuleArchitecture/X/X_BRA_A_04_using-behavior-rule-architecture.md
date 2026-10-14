# How Do You Actually Use a Behavior Rule Architecture?

**Behavior Rule Architecture — Main Series 04 / 06**

[[X_BRA_A_04-0.png]]

An architecture can define atomic Rules, schemas, classifications, Rulesets, and a Rule Library.

Then a practical question appears: how does a coding agent receive the right Rules for the task it is performing now?

The answer evolved from copying Rules into prompts to resolving a minimal execution view from an authoritative Library.

## Select by development scenario

Requirements work, source generation, test maintenance, and structural refactoring do not need identical behavioral constraints.

The early usage model was simple:

```text
Development Task
  -> Identify Scenario
  -> Select Ruleset
  -> Provide Rules
  -> Perform Task
```

This was better than one universal prompt. It allowed the development scenario to determine which Ruleset applied.

But complete Rules had become rich engineering objects. They contained identity, version, normative meaning, ownership, intent, responsibilities, applicability, and governance information. Sending all of that to the model on every inference consumed context and introduced material irrelevant to the immediate action.

## Preserve one Rule, project a smaller view

The complete Rule and its execution representation do not have to be identical.

The Rule Library can preserve the governed artifact:

```text
ID + Version + Normative
+ Owner + Intent + Applicability
+ Governance and lifecycle information
```

The execution view may need only:

```text
ID + Version + constrained instruction
```

Both represent the same Rule for different consumers. Governance information remains available without filling every model context.

That separation turns the Rule Library into infrastructure rather than a folder of prompt fragments.

## Resolve instead of copying

Maintaining separate compact Rule files creates version drift. The Library may contain `CODE-TI-01 v1.2` while a scenario file still delivers v1.1.

Low update frequency reduces the chance of failure. It does not remove the synchronization dependency.

A preprocessing Skill can resolve the current Ruleset when a task starts:

```text
Development Intent
  -> Identify Scenario
  -> Resolve Applicable Rules
  -> Retrieve Current Versions
  -> Build Minimal Execution View
  -> Continue the Task
```

The execution view becomes a derived artifact rather than another source of truth.

The practical evolution is:

```text
Copy Rules -> Reference Rules -> Resolve Rules
```

## Keep architecture independent of consumers

A Skill is one way to consume BRA. It is not BRA itself.

The dependency should run in this direction:

```text
BRA
  -> Rule Library
  -> Consumer
     ├── Skill
     ├── CLI
     └── CI or other tooling
  -> Project
```

A Validator controls the quality of Rules entering the Library. A Skill resolves Rules for an AI workflow. A CLI lets people or software inspect, validate, retrieve, or resolve the same assets.

Each layer can change without forcing a change to the normative Rule.

This usage model still leaves an important limit. Delivering the correct Rule proves neither that it influenced a decision nor that the resulting behavior complied with it. That requires decision evidence and evaluation.

## Start with the smallest useful infrastructure

Not every team needs a dedicated service, Skill, and CLI on day one.

A small team can begin with a version-controlled Library, validated Rule files, and one reproducible resolver that produces a task-specific view. The important properties are a single authoritative source, exact versions, controlled changes, and a record of what was delivered.

More infrastructure becomes justified when several projects consume the Library, manual selection creates errors, or different tools need consistent access. Automation should remove a demonstrated synchronization or delivery problem—not hide an unclear Rule model behind another layer.

This keeps the implementation proportional while preserving a path from simple files to shared infrastructure.

In your AI workflow, are execution instructions copied from a governed source—or resolved from it at the moment of use?

## Source

- [Contract Coding Skill](https://github.com/NextEvoEco/contract-coding-skill)

#BehaviorRuleArchitecture #AIEngineering #DeveloperTools #CodingAgents
