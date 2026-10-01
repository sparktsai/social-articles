# A Rule Cannot Govern an AI Development Decision If You Cannot Prove It Applied

## A rule can exist in the repository, appear in the final explanation, and still have had no observable effect on the decision.

[[M_EBG_A_05-0.png]]

An engineering team has a clear rule for payment retry changes:

> A retry implementation MUST preserve the existing idempotency key.

The rule is documented and version-controlled. An AI agent later changes the payment client, and the resulting code preserves the key. In its final summary, the agent even says it followed the rule.

Then a reviewer asks:

- Which rule version applied?
- Why did it apply to this change?
- Was it delivered before the retry design was selected?
- Did it eliminate an alternative or change the selected design?
- What evidence proves satisfaction rather than accidental conformity?
- If another rule conflicted with it, who could decide which one prevailed?

The team can show that the rule existed. It cannot yet show that the rule governed the decision.

That is the governance problem:

> If a rule has no identifiable version, applicability condition, Scope binding, invocation evidence, evaluation criteria, and authority path, governance cannot distinguish an applied rule from available guidance or a retrospective explanation.

---

## 1. Governance Problem: Rule Existence Is Not Rule Application

Open almost any AI-assisted development repository today and you will find rules everywhere.

Teams place them in system prompts, custom instructions, `AGENTS.md`, repository guidance, coding standards, security checklists, specifications, and review templates. Tools can automatically add some of those instructions to an agent's context.

That is already an improvement. A constraint no longer has to be repeated in every prompt.

The trouble starts when we assume that saving the rule also means the rule did its job:

```text
The rule existed
    therefore it was available
    therefore it was delivered
    therefore it applied
    therefore the decision complied
    therefore the decision was governed
```

It looks reasonable. Yet every arrow can fail.

A repository may contain several overlapping instruction files. A path rule may match the edited file but miss a behavior that crosses components. A rule may enter context without being relevant to the current Change Scope. Two applicable rules may conflict. The final code may comply even though the decision maker never received the rule.

So before we call the decision governed, we need to separate six states:

```text
Defined
    The rule has an identifiable meaning and version

Applicable
    Its conditions match this decision and Scope

Invoked
    It entered the decision basis

Influential
    It constrained evaluation or selection

Evaluated
    Evidence supports satisfaction, violation, or uncertainty

Governed
    An authorized role judged the finding and acted
```

Seen this way, the issue is not mainly whether the rule was written well. The issue is whether its path through the decision can be observed.

[[M_EBG_A_05-1.png]]

---

## 2. Existing Solutions Make Parts of Rules Operational

Again, we are not starting from nothing. Current tools already solve several parts of the problem.

Repository instruction files make guidance persistent and reusable. GitHub Copilot supports repository-wide, path-specific, and agent instruction files. Cursor rules can be always included, attached by file patterns, selected by the agent, or invoked manually.

Those mechanisms improve delivery, but they also make the gap easier to see. A rule may be always attached, conditionally attached, manually invoked, or selected by the agent. In other words, stored does not automatically mean invoked.

Normative keywords such as `MUST` and `MUST NOT` help distinguish an obligation from advice. "Preserve the idempotency key" is stronger than "be careful with retries." But a strong keyword does not identify the relevant Scope, evidence, conflict rule, or exception authority.

Linters, tests, static analysis, and architecture checks can evaluate conditions that are visible in code or configuration. They can prove that an artifact passed a check. They usually cannot prove that the rule was present before a design choice or that it influenced candidate evaluation.

Policy-as-code systems go further. Open Policy Agent evaluates declarative policy against structured input. Cedar connects authorization policy to principals, actions, resources, and context. These systems demonstrate the value of explicit scope, conditions, and machine-evaluable decisions.

But authorization and infrastructure policy are not the same as governing how one AI-assisted software decision was formed.

At the organizational level, frameworks such as the NIST AI RMF call for policies and practices to be transparent, implemented, monitored, and connected to clear responsibilities. They establish the governance expectation, but not an event-level record showing that `RULE-X@v3` applied to `DECISION-Y`.

Put these approaches together and we can see what each contributes:

```text
Instruction files preserve and deliver guidance
Normative language states obligation or prohibition
Automated checks evaluate visible conditions
Policy-as-code evaluates structured policy
Governance frameworks assign organizational responsibility
```

What we still cannot see is how one specific rule traveled into one specific engineering decision.

---

## 3. What Existing Solutions Still Cannot Resolve

The first gap appears before any tool runs: we often mix guidance and rules in the same prose.

"Keep the implementation simple" may be useful advice. "The payment client MUST preserve the existing idempotency key across retries" is an obligation with a testable result. If both appear as ordinary prose, the agent and reviewer must infer which one is mandatory.

Next comes applicability. A repository-wide rule may be too broad, while a path-based rule may be too narrow. Payment semantics can span several files. What we need to know is why the rule applied to this decision under this Scope, not merely where its file was stored.

Even after applicability is clear, invocation remains a separate question. Article 04's Context Manifest can show that a rule was delivered. Article 02's Decision Behavior Evidence can show whether it appeared in candidate evaluation. Code review and tests can show whether the resulting artifact satisfies it.

These are different claims:

```text
Context evidence:
    the rule was delivered

Decision evidence:
    the rule participated in the choice

Artifact evidence:
    the resulting change satisfies the rule
```

Time adds another complication. Rules change. A prohibition can become an obligation, an exception can expire, or a rule can be retired. Git may preserve the history, but a Decision ID still needs to point to the exact version that was active.

Then there are conflicts and exceptions. One rule may require backward compatibility while another requires removal of an unsafe interface. A prompt cannot reliably decide priority or authority. If that resolution remains in chat, the effective rule set disappears with the conversation.

And this is the part that is easiest to miss: passing a check does not prove governed decision behavior. The payment code may preserve the key because it followed an existing pattern, not because the rule ever entered the decision.

Outcome compliance and decision-behavior compliance are separate governance claims.

---

## 4. Governance Scope and the Elements That Must Become Visible

To make this governable, we need to narrow the unit. This article stays inside the development stage and looks at one versioned rule in relation to one Decision ID and one approved Change Scope.

It does not attempt to govern every instruction available to the agent, private model reasoning, production behavior, or the complete legal interpretation of an organizational policy.

From a reader's point of view, the required Governance Engineering Elements answer six practical questions.

### Which rule are we talking about?

The rule needs a stable ID, version, lifecycle state, owner, source, and one clear obligation or prohibition.

```text
<Subject> <MUST | MUST NOT> <Action> <Target> [Condition]
```

### Why does it apply here?

The rule needs conditions that explain when it applies: change type, system element, risk class, artifact, or decision category. It must also bind to the relevant VSS version and Change Scope.

VSS supplies the system state. Scope identifies the governed region for the current change. The rule states what must or must not occur inside that region.

### Which decision should it affect?

The record needs to identify the actor, choice, action, or artifact constrained by the rule and show whether the applicable version entered the decision basis before selection.

### How would we know what happened?

The rule needs an evidence expectation. What would support applicability? What would show invocation? What would demonstrate satisfaction or violation?

A positive obligation such as "tests MUST cover the retry path" needs evidence that the required thing exists. A prohibition such as "the change MUST NOT modify the public API" needs evidence that the forbidden change did not occur.

### What happens when rules conflict?

The effective ruleset needs a way to expose conflict, identify priority, request an exception, and name the authority allowed to decide.

### Can we follow the rule through the change?

The Rule ID must connect to VSS, Scope, Prompt Artifact, Context Manifest, Development Change ID, Decision ID, evidence, Audit Finding, and Governance Judgment.

None of this requires one universal file format. What matters is that the meanings stay stable and the relationships can be followed.

[[M_EBG_A_05-2.png]]

---

## 5. Engineering Design: From Rule Asset to Governance Judgment

This is where Behavior Rule Architecture, or BRA, becomes useful. It offers one path from broad intent to atomic, versioned rules and reusable rulesets.

The full path is:

```text
Intent
    -> normative statement
    -> versioned rule
    -> applicable ruleset
    -> decision invocation
    -> evidence
    -> audit finding
    -> governance judgment
```

The early stages give us a well-engineered rule. They still do not prove that the rule governed a particular decision.

Start with a distinction people can read immediately: intent describes what we want; a rule states what must or must not happen.

```text
Intent:
    "Retries should be safe."

Rule:
    "Payment retry implementation MUST preserve the existing
     idempotency key for every retry attempt."
```

Next, store the rule as a versioned asset. Rulesets should point to exact versions rather than copy the wording around. Git preserves the history; the development record tells us which point in that history mattered.

Only then do we ask whether it applies to the current change. That answer comes from the VSS system state, Change Scope, change classification, and the rule's own conditions:

```text
VSS + Scope + change classification
    -> applicable rule versions
```

The effective ruleset must enter the development basis before the relevant decision. Evidence should distinguish whether the rule was discoverable, selected as applicable, delivered, used in evaluation, and satisfied by the result.

At that point, Audit can compare the rule state we expected with the evidence we actually captured:

```text
Expected:
    VSS + Scope + applicable rule + evidence expectation

Observed:
    Context Evidence + Decision Evidence + artifact verification

Audit:
    satisfied | violated | not invoked | conflict | insufficient evidence

Governance:
    accept | reject | correct | approve exception | escalate
```

This is how Articles 02 through 05 connect:

```text
Article 02 asks what happened around one decision
Article 03 gives each fine-grained engineering unit a role-aware, versioned, and timestamped trace
Article 04 asks what system and change basis was supplied
Article 05 asks which rule applied and what the evidence supports
```

Together they create governance infrastructure. Governance occurs only when an authorized process uses that infrastructure to judge and act.

[[M_EBG_A_05-3.png]]

---

## 6. Example: Auditing One Rule Against One Payment Retry Decision

Let us take the same payment retry decision and keep only the fields needed to see the distinction.

```yaml
development_change:
  id: CHG-payment-retry-184
  trace_id: TRACE-payment-retry-184
  vss: VSS-payment-system@v12
  scope: SCOPE-payment-retry@v4
  decision_id: CODE-DEC-042

rule:
  id: RULE-PAYMENT-IDEMPOTENCY@4.0.0
  statement: >
    Payment retry implementation MUST preserve the existing
    idempotency key for every retry attempt.
  applies_when:
    change_type: modify-retry-behavior
    system_element: payment-client
  evidence_expected:
    - rule delivered before CODE-DEC-042
    - candidate evaluation shows the rule's effect
    - review and test verify key reuse

observed:
  available_in_repository:
    status: verified
    evidence: GIT-rule-library@8d31f2a
  selected_as_applicable:
    status: verified
    evidence: EVT-rule-resolution-118
  delivered_before_decision:
    status: not-captured
  cited_in_final_summary:
    status: declared
    evidence: EVT-agent-summary-241
  influence_on_evaluation:
    status: unknown
  artifact_satisfaction:
    status: verified
    evidence: [REVIEW-payment-184, TEST-idempotency-retry-092]

audit:
  - finding: rule-invocation-not-proven
    detail: No evidence shows delivery before CODE-DEC-042.
  - finding: artifact-satisfies-rule
    detail: Review and test verify idempotency-key reuse.

governance_judgment:
  authority: human:payment-maintainer
  decision: accept-code-with-process-nonconformity
  actions:
    - record that artifact compliance is proven but invocation is not
    - require ruleset binding in the next Context Manifest
    - audit the next three payment decisions
```

The interesting part is that this record supports two conclusions at the same time.

First, the resulting code satisfies the idempotency requirement. Review and test evidence support that claim.

Second, the organization cannot prove that the rule governed the formation of `CODE-DEC-042`. The rule existed and was cited later, but its delivery before the decision and its effect on candidate evaluation were not captured.

That leaves a real governance choice. The authorized maintainer may accept the code while recording a process nonconformity. A stricter risk policy may reject it. Evidence does not choose the response; it gives the responsible authority a sound basis for choosing.

```text
Rule engineering makes the normative state identifiable
Evidence supports claims about application and result
Audit separates compliance from unsupported claims
Governance decides and acts
```

A rule in a file is an asset. Connected to Scope, decision behavior, evidence, audit, and authority, it becomes governance infrastructure. It becomes governance only when an authorized judgment is made and acted upon.

---

## References

- [GitHub Docs: Adding custom instructions for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions)
- [Cursor Docs: Rules](https://docs.cursor.com/context/rules)
- [RFC 2119: Key Words for Use in RFCs to Indicate Requirement Levels](https://www.rfc-editor.org/info/rfc2119/)
- [Open Policy Agent Documentation](https://www.openpolicyagent.org/docs)
- [Cedar Policy Language Reference Guide](https://docs.cedarpolicy.com/)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)

### Related Work by the Author

- [Spark Tsai, *Behavior Rule Architecture: Rule-Based Governance of AI System Behavior*](https://doi.org/10.31224/6681)
- [Spark Tsai, *Viewpoint-Structured Specification (VSS)*](https://doi.org/10.31224/6612)
- [Spark Tsai, *Scope as a Governance Primitive: Making Inference, Authority, Effect, and Evidence Explicit in AI Governance*](https://doi.org/10.5281/zenodo.22108234)
- [Spark Tsai, *Toward Decision Behavior Governance: Governance Existence, Invocation, and Decision Formation*](https://doi.org/10.5281/zenodo.18876165)
- [Spark Tsai, *Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development*](https://doi.org/10.31224/6616)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
