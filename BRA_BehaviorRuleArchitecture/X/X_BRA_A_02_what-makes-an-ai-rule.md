# What Makes an AI Instruction a Rule?

**Behavior Rule Architecture — Main Series 02 / 06**

[[X_BRA_A_02-0.png]]

Moving an instruction from a prompt into a file makes it reusable. It does not automatically make it a Rule.

“Please avoid changing unrelated code.”

“You should not change unrelated code.”

“You must not change unrelated code.”

They point in the same direction, but they do not express the same normative force. A model still has to infer whether each sentence is a preference, recommendation, obligation, or prohibition.

## Structure before interpretation

Natural language is expressive because its structure is flexible. That flexibility increases the interpretation required each time an instruction is consumed.

Normative Natural Language (NNL) reduced the structural variation by exposing components such as:

```text
Actor + Normative Expression + Action + Target + Condition
```

Constraint Normative Language (CNL) then narrowed the normative vocabulary. For the development behavior I needed to control, the useful distinction eventually became:

```text
MUST     -> required behavior
MUST NOT -> prohibited behavior
```

This does not make an instruction executable. It makes its intended polarity explicit enough to represent independently.

## Name the governed behavior

Polarity alone is insufficient. Consider a task to fix source code until existing tests pass.

If the test files are also available for modification, the AI can make the failure disappear by changing an assertion instead of correcting the implementation.

The outcome—passing tests—looks successful. The development behavior is wrong.

A more precise constraint is:

> AI MUST NOT modify test code when fixing source code unless test modification is explicitly authorized.

It exposes three important parts:

```text
MUST NOT -> normative polarity
modify   -> governed action
test_code -> governed target
```

The Rule now describes behavior, not merely a desired result.

## Keep behavior separate from applicability

The same principle may apply to source code, tests, documents, configuration, or schemas. Creating a separate Rule for every target duplicates the behavioral meaning.

The Rule can remain stable while its applicable range changes.

That range also depends on more than Target. Modifying tests may be prohibited while fixing an implementation, permitted while updating an obsolete test, and required while adding feature coverage.

So two questions must remain separate:

```text
What behavior is required or prohibited?
-> Rule

Under which conditions does it apply?
-> Applicability
```

This separation prevents each new task context from becoming another near-duplicate Rule.

## A Rule is a stable behavioral object

Within AI-assisted software development, a Rule can therefore be defined as:

> A structured statement describing required or prohibited behavior, separated from the conditions under which that behavior applies.

This definition does not guarantee compliance or enforcement. It does something more foundational: it exposes enough meaning that another model, session, or workflow does not have to reconstruct the behavioral intent from scratch.

Once that stability exists, new questions appear: identity, version, owner, lifecycle, composition, and evidence. Those are the questions that turn a Rule into an engineering object.

## Precision should not pretend the world is simple

Reducing normative vocabulary does not mean every engineering expectation can be expressed responsibly as one unconditional `MUST` or `MUST NOT`.

Some behavior depends on authority, phase, risk, or exceptions. Those conditions should be represented explicitly instead of hidden behind a softer verb. When the team genuinely wants a recommendation rather than an obligation, it should not mislabel the preference as a Rule merely to sound decisive.

Atomicity also matters. “Modify only authorized files, preserve all interfaces, update tests, and document the change” contains several independently applicable constraints. Splitting them allows each behavior to have its own version, applicability, evidence, and exception path.

The objective is not rigid language for its own sake. It is a representation whose intended force and governed behavior can be inspected without guessing.

Choose one instruction your team reuses. Can you identify its polarity, action, target, and applicability without interpreting the entire paragraph again?

#BehaviorRuleArchitecture #BehaviorRules #AIEngineering #SoftwareEngineering
