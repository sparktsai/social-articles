# The Governed AI Rule and the Model’s Execution View Should Not Be Identical

**Behavior Rule Architecture — Problem Deep Dive 05 / 08**

[[X_BRA_A_11-0.png]]

A complete behavioral Rule may contain identity, version, normative meaning, ownership, intent, applicability, responsibilities, evidence expectations, and lifecycle information.

Does the model need all of that for every coding decision?

Usually not. But deleting it to save context weakens governance.

The better design preserves the complete Rule as the authoritative asset and derives a smaller execution view for the current task.

## Different consumers need different representations

Governance needs to know who owns the Rule, why it exists, which version is active, and how it should be reviewed.

An LLM performing a bounded coding task primarily needs the constraint it must follow and enough identity to preserve traceability.

Conceptually:

```text
Complete Rule
├── ID and version
├── normative constraint
├── owner and intent
├── applicability information
├── governance impact
└── lifecycle and evidence metadata

        -> projection

Execution View
├── ID
├── version
└── constrained instruction
```

The projection is not a second Rule. It is a purpose-specific representation of the governed Rule.

## Stored projections create drift

An early approach is to keep full Rules in a repository and maintain compact scenario files beside them.

That works until the Library advances to v1.2 while a compact file still contains v1.1.

The problem is not merely which copy is current. A reviewer must know which version the model actually received.

Manual synchronization can reduce drift, especially when Rules change infrequently. It cannot remove the dependency created by two maintained sources.

## Derive the view at use time

A preprocessing consumer can resolve the task’s Ruleset from the authoritative Library, retrieve exact versions, and build the compact view when the task begins.

```text
Task and approved context
  -> Resolve applicable Rules
  -> Retrieve authoritative versions
  -> Project required execution fields
  -> Deliver to model
  -> Record delivered view
```

Now the compact representation is disposable. It can be regenerated and does not compete with the Rule Library as a source of truth.

## Projection needs its own integrity checks

Deriving a view does not automatically make delivery trustworthy.

The workflow should verify that selected IDs resolve, versions match, required normative content survives projection, and the delivered manifest records what reached the model.

Sensitive governance information can remain outside the model context while still being resolvable to an authorized reviewer.

The smallest execution view is not always the best one. If applicability conditions or conflict resolutions are necessary to interpret the constraint, omitting them creates ambiguity. Minimize what is irrelevant, not what is necessary.

The architectural principle is simple: **preserve one governed Rule, then create consumer-specific views without turning those views into independent truth.**

## A view should be traceable in both directions

From an execution record, a reviewer should be able to resolve the complete Rule version that produced the view.

From the governed Rule, an authorized reviewer should be able to identify which tasks received a particular version when that history is required.

This does not mean storing sensitive prompts or full governance metadata everywhere. A manifest can retain IDs, versions, hashes, projection method, and controlled references.

Bidirectional traceability makes two checks possible: whether the model received a faithful projection, and whether a later Rule revision affects only future executions rather than silently changing the basis of historical ones.

It also lets teams compare two consumers without assuming that identical Rule IDs produced identical delivered context.

Does your current AI workflow resolve execution instructions from an authoritative source—or maintain another copy that can silently drift?

#BehaviorRuleArchitecture #ContextEngineering #AIEngineering #RuleLibrary
