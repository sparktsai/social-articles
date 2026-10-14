# How Do You Know the AI Actually Followed the Rule?

**Behavior Rule Architecture — Main Series 05 / 06**

[[X_BRA_A_05-0.png]]

An AI coding agent receives this Rule:

> AI MUST NOT modify test code unless test modification is explicitly authorized.

The implementation is fixed. Tests pass. Test files remain unchanged.

Did the Rule work?

The result is compatible with the Rule. It does not prove the Rule caused the decision, entered candidate evaluation, or was even relevant to the path the model selected.

## Good output is not process evidence

Three distinctions matter:

```text
Good Result != Rule Compliance
Rule Loaded != Rule Triggered
Rule Triggered != Rule Followed
```

A final diff shows what changed. It cannot, by itself, reconstruct which constraints were active, which alternatives appeared, or why one option was selected.

To govern development behavior, preserve the decision that produced the artifact—not only the artifact.

## Connect the Rule to a bounded decision

Decision Evidence can retain:

- the decision point and context;
- input artifacts and constraints;
- candidate options when observable;
- the selected option and recorded rationale;
- expected impact and trace relationships;
- applicable Rule IDs and versions.

The useful relationship is not merely:

```text
Task -> Ruleset -> Result
```

It is:

```text
Rule -> Decision Behavior -> Evidence -> Artifact
```

This makes the information needed for governance observable. It does not yet create governance.

## Review attention must be selective

One coding task may contain decisions about files, interfaces, dependencies, tests, error handling, and architecture. Recording each decision can create more evidence than anyone can realistically review.

Reviewing everything turns observability into an evidence backlog.

Decision Risk provides a selection mechanism:

```text
Observe Decision
  -> Detect Risk Signal
  -> Locate Relevant Evidence
  -> Review That Decision
```

Suppose a source-code repair unexpectedly changes a test expectation. The effect crosses the task’s expected boundary. That signal identifies the decision worth inspecting; evidence reveals the applicable Rule, context, candidates, and result.

Risk does not prove wrongdoing. It provides a reason to direct limited human attention toward a specific decision.

## Evidence enables governance; authority performs it

Storing evidence does not determine whether a Rule was effective, whether an exception is justified, or what should happen next.

Governance begins when an authorized role can use a signal and its evidence to accept, correct, escalate, or revise the work.

Actual use may also show that the Rule—not the agent—needs improvement. A condition may be ambiguous, a boundary too broad, or two Rules may interact unexpectedly.

This is why Rule identity and version matter operationally. Historical evidence must resolve to the Rule semantics that existed when the decision occurred, not whatever the Rule says today.

A reusable Rule becomes governable when usage produces observable evidence, meaningful signals direct review, and review can lead to an authorized action.

## Do not overclaim internal influence

Even detailed Decision Evidence usually describes external, recorded behavior. A delivered Rule, a visible candidate comparison, and a generated rationale can support a claim about the workflow’s observable decision path.

They do not expose every internal influence on a model or prove that one token sequence caused the result. The evidence claim should stay within that boundary.

Artifact verification remains independently valuable. Tests may show that the result satisfies a Rule even when the process record is incomplete. Conversely, delivery and visible evaluation may be captured while the final artifact still violates the constraint.

Reporting those findings separately produces a more honest review than collapsing them into one “followed” status.

For one Rule in your current workflow, can you trace from its exact version to the decision it constrained and the evidence used to judge the result?

## Source

- [Decision Risk](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6655398)

#BehaviorRuleArchitecture #AIGovernance #DecisionEvidence #ContinuousImprovement
