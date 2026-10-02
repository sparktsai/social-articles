# Your AI Followed the Rule. Can You Show How?

**Engineering Before Governance | 05 / 08**

Your repository contains a rule: payment retries must preserve the existing idempotency key.

The AI-generated code preserves the key. Tests pass. The final summary says the rule was followed.

What can you conclude?

You may have evidence that the artifact satisfies the rule. You still need separate evidence to claim that this rule version entered the decision basis and participated in the recorded choice.

[[L_EBG_A_05-0.png]]

## A rule file leaves several questions open

Persistent instructions make constraints easier to reuse. Normative wording makes obligations clearer. Tests, linters, static analysis, and policy evaluation can check specific conditions.

These are useful capabilities, but they support different parts of a rule's path through development.

A rule can be stored without being delivered. It can be delivered without applying to the current decision. It can apply while conflicting with another rule. The result can satisfy it even when no evidence establishes its participation in the choice.

Treating all those states as "followed" makes later review ambiguous.

## Separate six states before making a claim

**Defined:** the rule has an identifiable meaning and version.

**Applicable:** its conditions match the decision and approved Change Scope.

**Invoked:** evidence establishes that it entered the relevant decision basis.

**Influential:** observable evaluation shows how it constrained a candidate or selection. This remains a claim about recorded behavior, with limits on what can be established about internal model influences.

**Evaluated:** evidence supports satisfaction, violation, conflict, or uncertainty.

**Governed:** an authorized role judged the finding and acted.

These distinctions make it possible to report artifact compliance and a process evidence gap together, instead of forcing the entire change into one yes-or-no label.

## Engineer the rule before auditing its application

Start with an atomic obligation or prohibition:

> Payment retry implementation MUST preserve the existing idempotency key for every retry attempt.

Give it a stable ID, exact version, lifecycle state, and owner. Specify its applicability conditions and the Scope it constrains. Separate the intent, "retries should be safe," from the requirement someone can evaluate.

Behavior Rule Architecture (BRA) provides one approach to organizing versioned rules and reusable rulesets. For a specific change, the effective ruleset should reference exact rule versions.

Then define the evidence expectation. Delivery evidence supports that the rule reached the decision basis. A recorded candidate evaluation supports a claim about its visible role in selection. Review and tests support a claim about the resulting artifact.

A conflict or exception also needs an authority path. If compatibility and security requirements conflict, the record must identify who may resolve that conflict and what effective rule set follows. A resolution left only in chat can disappear from the basis of later work.

## One payment change can support two conclusions

Consider a retry change with the following evidence:

- rule version 4 exists in the library and was selected as applicable;
- delivery before the decision was not captured;
- the final agent summary cites the rule;
- review and tests verify reuse of the existing key.

The artifact satisfaction claim is supported. The invocation claim remains unproven.

An authorized maintainer might accept the code while recording a process nonconformity, require ruleset binding in the next Context Manifest, and audit subsequent payment changes. A stricter policy may require a new generation or additional review before acceptance.

The evidence provides the basis for that choice. It does not determine the response automatically.

[[L_EBG_A_05-3.png]]

## Ask for the rule-to-decision connection

Link the Rule ID and version to the approved Scope, context delivery, Decision ID, generated artifact, verification, audit finding, and governance action.

When an event is missing, preserve that limitation. A later summary cannot retroactively establish delivery before an earlier decision.

This also suggests how to improve the process. Missing delivery evidence calls for better context capture. Conflicting obligations call for explicit resolution. An artifact violation calls for correction and verification. Each finding points to a different action.

On your next AI-assisted review, replace "Did it follow our rules?" with three questions: which version applied, what evidence shows its recorded application, and what evidence verifies the result?

The answers make the review more precise and the follow-up more useful.

## Further Reading

- [RFC 2119: Requirement Levels](https://www.rfc-editor.org/info/rfc2119/)
- [Spark Tsai: Behavior Rule Architecture](https://doi.org/10.31224/6681)
- [Spark Tsai: Toward Decision Behavior Governance](https://doi.org/10.5281/zenodo.18876165)
