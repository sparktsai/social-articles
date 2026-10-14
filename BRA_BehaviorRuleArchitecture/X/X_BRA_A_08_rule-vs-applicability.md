# The Rule and Where It Applies Are Different Engineering Objects

**Behavior Rule Architecture — Problem Deep Dive 02 / 08**

[[X_BRA_A_08-0.png]]

Suppose a team wants AI coding agents to avoid modifying artifacts outside the requested change.

It could write one Rule for source code, another for tests, another for documents, and another for configuration.

The list grows, but the behavioral principle has not changed. Only its application context has.

That is a sign that the Rule and its applicability have been collapsed into the same object.

## Repeating Targets creates false variety

Consider these constraints:

```text
AI MUST NOT modify unrelated source_code.
AI MUST NOT modify unrelated test_code.
AI MUST NOT modify unrelated document.
AI MUST NOT modify unrelated configuration.
```

They look like four Rules. They may be one stable behavioral constraint applied across four Targets.

If every new artifact type produces another copy, the Rule collection grows as:

```text
Action x Target x Context x Stage
```

That is not meaningful behavioral diversity. It is contextual duplication.

## Target alone does not determine applicability

The same Target can be permitted or prohibited depending on the task.

For `test_code`:

```text
Fix implementation against existing tests
-> test modification not authorized

Update an obsolete test
-> test modification authorized

Add coverage for a new feature
-> test creation required
```

A blanket Rule saying AI may never modify tests would be too broad. A Rule that embeds every possible task condition would become too specific to reuse.

The more stable design separates two questions:

```text
What behavior is required or prohibited?
-> Rule

Under which task, role, target, stage, scope, and condition?
-> Applicability
```

## Bind dynamic boundaries at use time

An atomic Rule can express the behavioral constraint. The development workflow can bind the current scope and select the Rule when its conditions match.

For example:

```text
Task intent: fix source implementation
Authorized targets: source_code
Excluded targets: test_code
Applicable Rule: preserve test independence
```

Another task can bind a different scope without rewriting the Rule itself.

This keeps the behavioral meaning versionable and reusable while allowing the execution boundary to change with the authorized work.

## Applicability needs evidence too

Selecting a Rule requires a supportable basis. Which task intent, role, target, or stage caused it to apply? Which scope version was active? Was an exception authorized?

A record that says only “Rule loaded” cannot answer those questions.

Likewise, a Rule may exist and be valid while not applying to a particular decision. Treating every stored Rule as universally active overloads context and creates apparent conflicts that the task never needed to resolve.

The goal is not fewer Rules at any cost. Distinct behavioral meanings deserve distinct Rules. Contextual variation should remain contextual.

## Avoid moving all complexity into applicability

Separation can fail in the opposite direction too. A vague Rule such as “AI MUST behave safely” remains vague even if it has a sophisticated applicability model.

The atomic Rule still needs a recognizable action, target, and normative meaning. Applicability should select a stable constraint, not complete an unfinished one differently in every workflow.

A practical test is to read the Rule without the current task. Its behavioral obligation should remain understandable. Then read the applicability record without rewriting the Rule. It should explain why that obligation is relevant here.

When both objects can be understood and versioned separately, the Rule can travel across contexts without losing its meaning, and the context can change without creating a new Rule.

Choose two nearly identical Rules in your Library. Do they express different behavior—or the same behavior bound to different applicability conditions?

#BehaviorRuleArchitecture #BehaviorRules #AIEngineering #SoftwareArchitecture
