# Your AI Followed the Rule. Can You Show How?

**Engineering Before Governance — Main Series 05 / 08**

[[X_EBG_A_05-0.png]]

Your repository contains a rule: payment retries must preserve the existing idempotency key.

The AI-generated code preserves the key. Tests pass. The final summary says the rule was followed.

What can you conclude?

You may have evidence that the artifact satisfies the rule. You still need different evidence to claim that this rule version entered the decision basis and participated in the recorded choice.

## A rule file leaves several questions open

Persistent instructions make constraints reusable. Normative wording clarifies obligations. Tests, linters, static analysis, and policy evaluation can check specific conditions.

But those capabilities support different parts of a rule’s path through development.

A rule can be stored without being delivered. It can be delivered without applying to the current decision. It can apply while conflicting with another rule. The result can satisfy it even when no evidence establishes its participation in the choice.

Calling all those states “followed” makes later review ambiguous.

## Separate six states

Before making a compliance claim, distinguish:

1. **Defined:** the rule has an identifiable meaning and version.
2. **Applicable:** its conditions match the decision and approved Change Scope.
3. **Invoked:** evidence establishes that it entered the relevant decision basis.
4. **Influential:** observable evaluation shows how it constrained a candidate or selection.
5. **Evaluated:** evidence supports satisfaction, violation, conflict, or uncertainty.
6. **Governed:** an authorized role judged the finding and acted.

“Influential” remains a claim about recorded external behavior. It does not reveal every internal model influence.

These distinctions let a team report artifact compliance and a process evidence gap together instead of forcing the entire change into one yes-or-no label.

## Engineer the rule before auditing it

Start with an atomic obligation:

> Payment retry implementation MUST preserve the existing idempotency key for every retry attempt.

Give it a stable ID, exact version, lifecycle state, and owner. Define applicability conditions and the scope it constrains. Separate the intent—“retries should be safe”—from the requirement someone can evaluate.

For a specific change, the effective ruleset should reference exact rule versions.

Then define the evidence expectation. Delivery evidence supports that the rule reached the decision basis. A recorded candidate evaluation supports a claim about its visible role in selection. Tests and review support a claim about the resulting artifact.

Conflicts and exceptions need an authority path. If compatibility and security requirements conflict, record who may resolve that conflict and which effective ruleset follows. A resolution left only in chat can disappear from later work.

## One change can support two conclusions

Consider a retry change where:

- rule version 4 exists and was selected as applicable;
- delivery before the decision was not captured;
- the final agent summary cites the rule;
- review and tests verify reuse of the existing key.

The artifact satisfaction claim is supported. The invocation claim remains unproven.

An authorized maintainer might accept the code while recording a process nonconformity, require ruleset binding in the next Context Manifest, and inspect later payment changes. A stricter policy might require a new generation.

Evidence supports that choice. It does not determine the response automatically.

## Ask for the connection

Link the Rule ID and version to approved scope, context delivery, Decision ID, generated artifact, verification, finding, and governance action.

When an event is missing, preserve the limitation. A later summary cannot retroactively establish delivery before an earlier decision.

Different gaps also require different fixes. Missing delivery evidence calls for better capture. Conflicting obligations call for explicit resolution. An artifact violation calls for correction and verification.

On your next AI-assisted review, replace “Did it follow our rules?” with three questions: which version applied, what evidence shows its recorded application, and what verifies the result?

## Sources

- [RFC 2119: Requirement Levels](https://www.rfc-editor.org/info/rfc2119/)
- [Behavior Rule Architecture](https://doi.org/10.31224/6681)
- [Toward Decision Behavior Governance](https://doi.org/10.5281/zenodo.18876165)

#EngineeringBeforeGovernance #AIGovernance #BehaviorRules #SoftwareEngineering
