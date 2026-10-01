# You Cannot Control Decision Risk If Risk Exists Only as a Score

## A red cell in a risk matrix does not show which development decision created the risk, what evidence supports it, or whether a control actually reduced it.

[[M_EBG_A_06-0.png]]

An AI agent changes the retry behavior of a payment client.

The code passes its focused tests. The pull request is labeled `medium risk` because it touches payment logic. A reviewer adds two comments, the agent makes another change, and the pull request eventually turns green.

That sounds like risk control.

But the team still cannot answer:

- Which part of the decision behavior created the risk?
- Was the risk caused by missing context, an out-of-scope change, an untriggered rule, or the selected design itself?
- What engineering effect could follow from that condition?
- Which control was meant to prevent, detect, or correct it?
- Did the control actually change the decision or only add another approval?
- What risk or uncertainty remained after the correction?

The team has a risk label. It does not yet have an engineering-visible risk condition.

That is the governance problem:

> If decision risk is represented only by a category, score, or reviewer concern, governance cannot trace the risk back to observable decision behavior, apply a targeted control, or demonstrate that the risk was reduced.

Before risk can be governed, engineering must make the condition behind the risk visible.

---

## 1. Governance Problem: A Risk Rating Is Not Yet a Controllable Risk

Look at most software development processes and you will find familiar risk signals: a high-risk ticket, a red item in a risk register, a security finding, a failed test, a large diff, or a reviewer saying, "This change feels dangerous."

These signals are useful. They tell us where to look.

What they often do not tell us is what, exactly, should be controlled.

A score such as `Likelihood 3 × Impact 4 = High` compresses several questions into one label. Was required architecture context missing? Did the generation modify an artifact outside Scope? Did a rule trigger and get ignored? Was an assumption left unresolved? Did the selected design create a coupling that the original request never authorized?

Those conditions call for different controls.

More review will not repair missing context. A test cannot prove that a rule participated in the decision. Requiring approval does not show whether the generated code remained inside Scope. Blocking every high-scoring change may reduce activity without reducing the underlying risk.

So the goal is not to produce a more elaborate risk score. It is to identify the engineering condition that makes one development decision risky and connect it to evidence and treatment.

This also sets an important boundary:

> Decision Risk does not mean that the generated document or code is already wrong.

A change can pass tests and still carry decision risk because its origin, boundary, rule application, or effect cannot be established. Conversely, a visible defect is not automatically a decision-governance failure; it may be an ordinary implementation error with clear provenance and effective correction.

[[M_EBG_A_06-1.png]]

---

## 2. Existing Solutions Already Manage Important Parts of Risk

Risk management is not new, and software teams already have several mature practices.

ISO 31000 provides a general process for identifying, analyzing, evaluating, treating, monitoring, and communicating risk. The NIST AI Risk Management Framework organizes work through Govern, Map, Measure, and Manage, and explicitly connects risk measurement to prioritization and treatment.

Secure development frameworks such as NIST SSDF bring risk-based practices into the software lifecycle. Threat modeling helps teams ask what can go wrong before implementation. Code review, static analysis, dependency scanning, tests, and quality gates detect specific problems in engineering artifacts.

Risk registers and matrices help organizations compare and prioritize concerns. Change classifications help route sensitive work to additional review. Architecture review boards and security gates provide escalation paths for consequential changes.

Requirements Traceability Matrices, or RTMs, solve another important part of the problem. A maintained bidirectional RTM connects requirements to downstream design elements, code, tests, and verification results. When a requirement changes, the trace can reveal which engineering artifacts may need review or modification.

That makes RTM one of the practical foundations for change impact analysis:

```text
Requirement change
    -> related design
    -> affected code
    -> required tests
    -> verification evidence
```

Put together, these practices cover a great deal:

```text
Risk frameworks organize identification, assessment, and treatment
Threat modeling anticipates possible failure paths
Engineering tools detect observable artifact problems
RTM preserves the requirement change and verification chain
Risk matrices help prioritize attention
Review and gates decide whether work may proceed
```

The problem is not that these methods are weak. The problem is that they often operate at the project, system, vulnerability, or release level.

The decision that shaped one generated document or code change can remain hidden underneath them.

RTM can show that a payment requirement traces to a design component, implementation module, and test case. It does not automatically show that those artifacts entered the LLM context, that the requirement influenced a generated alternative, or that a particular rule triggered during the decision.

---

## 3. What Existing Solutions Still Cannot Resolve

The first gap is granularity.

A project risk register may say `payment integrity risk`. A scanner may report a code weakness. A reviewer may flag a large change. None of those records necessarily identifies the specific development decision that created the exposure.

The second gap is the difference between traceability and actual decision behavior.

RTM gives us the declared requirement change chain. It is excellent for asking, "If this requirement changes, which design, code, and tests may be affected?" But a trace link does not prove that the linked requirement was supplied to one AI generation or that it shaped the decision that produced the change.

This is why RTM and Development Evidence are complementary:

```text
RTM
    shows the declared requirement-to-artifact chain

Development Evidence
    shows what actually entered and occurred during generation
```

The third gap is interpretation.

Development Evidence from Article 02 may show that an alternative appeared and a rule triggered. Article 03 may connect that finding to a fine-grained role, version, timestamp, and related engineering elements. Article 04 may show that the architecture viewpoint was missing from the supplied context. Article 05 may show that the final code satisfies a rule even though rule invocation cannot be proven.

Those are observable findings. They are not yet risk judgments.

Someone still has to explain why the finding matters:

```text
Observed condition
    The architecture viewpoint was not supplied

Possible engineering effect
    The retry design may cross the shared transaction boundary

Decision risk
    The generated change may alter transaction semantics
    without a visible architecture basis
```

The fourth gap is treatment traceability.

Teams often record that a risk was "mitigated" after review, but the connection between risk and control remains vague. Which control addressed which condition? What evidence shows that it ran? Did it prevent the risky decision, detect it afterward, or correct the generated artifact?

The fifth gap is residual risk.

A corrected code diff does not necessarily repair missing decision evidence. A newly supplied rule does not prove that an earlier generation used it. A second review may lower concern without resolving the original uncertainty.

Finally, missing evidence is easily mistaken for low risk.

If no rule trigger was captured, that could mean no rule triggered. It could also mean the trigger was not observed. If no out-of-scope effect was recorded, that could mean the change stayed inside Scope or that the effect boundary was never measured.

No signal is not the same as no risk.

---

## 4. Governance Scope and the Decision Risk Elements That Must Become Visible

To keep the scope practical, this article looks at one development decision that contributes to a generated document or code artifact.

It does not attempt to predict every future production failure, calculate model confidence, or replace security and quality assessment. It asks a narrower question:

> What engineering-visible condition makes this decision a governance risk, and what would show that the condition was treated?

For this problem, the required **Decision Risk Engineering Elements** answer eight practical questions.

### Which decision is exposed?

Identify the Decision ID, Development Change ID, generated artifact, and Trace ID. A risk that cannot be attached to a specific decision remains a general concern rather than an actionable decision risk.

### What condition created the risk?

Use observable evidence rather than a generic label. Examples include:

- required context was not supplied;
- generated behavior exceeded Change Scope;
- a relevant rule triggered and was not followed;
- rule invocation cannot be demonstrated;
- alternatives exposed an unresolved trade-off;
- a generated effect has no traceable decision basis.

### What could be affected?

Name the engineering object and effect: an API contract, transaction boundary, data model, security assumption, test obligation, architecture dependency, or specification element.

### How does the impact propagate?

Use RTM, VSS relations, dependency links, and other maintained engineering traces to follow the change chain across requirements, design, code, tests, interfaces, and verification evidence.

Impact Analysis should distinguish direct impact from possible downstream impact. A requirement-to-code trace is evidence of a maintained relationship; it is not proof that every linked artifact was changed or that harm occurred.

### How could the condition become harmful?

Describe a credible path from the observed condition to an engineering consequence. This is more useful than writing `high impact` without explaining what the impact would be.

### What signal would reveal the risk?

Connect the risk to something observable: a missing Context Manifest entry, an out-of-scope diff, a triggered rule, an unresolved alternative, a failed trace, or a mismatch between the decision and generated artifact.

### Which control addresses it?

Identify whether the control is intended to prevent, detect, or correct:

```text
Prevent
    Supply required context or bind rules before generation

Detect
    Compare generated effects with Scope and triggered rules

Correct
    Regenerate, revise, revert, or explicitly resolve the decision
```

### What remains afterward?

Record the residual risk or unresolved uncertainty after the control. A risk is not closed merely because an action was performed.

These elements make risk inspectable without pretending that every judgment can be reduced to a number.

[[M_EBG_A_06-2.png]]

---

## 5. Engineering Design: Connect Evidence, Risk, Control, and Result

The engineering design begins with evidence from the earlier articles.

Article 02 records what actually happened during generation: supplied context, alternatives that appeared, rules that triggered, the decision, and the generated artifact.

Article 03 gives each fine-grained engineering unit a role-aware, versioned, and timestamped Trace ID so that evidence and relationships can be followed.

Article 04 compares the required development basis with what was actually supplied.

Article 05 determines which rule applied, whether it entered the decision, and what the available evidence can support.

Article 06 adds two engineering steps before risk treatment.

**Decision Analysis** examines the structural relationship between the approved Scope and the generated effect. It answers questions such as: did the change remain inside Scope, did an unsupported effect appear, and can the effect be traced to a visible decision basis?

**Impact Analysis** follows the affected engineering chain. RTM can carry the trace from requirements to design, code, tests, and verification. VSS and structural dependency links can extend that view across architecture viewpoints and interfaces.

**Decision Risk** interprets those analytical results as governance concerns and connects them to controls.

The combined path is:

```text
Development Evidence
    -> Decision Analysis
    -> Impact Analysis
    -> affected engineering chain
    -> Decision Risk
    -> targeted control
    -> control evidence
    -> residual risk
    -> governance judgment
```

The ordering matters.

If Decision Analysis has not identified the generated effect, Impact Analysis has no stable starting point. If the requirement and dependency chain is not traced, Decision Risk can exaggerate or overlook the affected surface. If risk is assigned before either analysis, the score becomes an opinion. If residual risk is not checked, `mitigated` becomes another unsupported claim.

The three layers answer different questions:

```text
Decision Analysis
    What did this decision change relative to its Scope?

Impact Analysis
    Which requirements, designs, code, tests, and interfaces can be affected?

Decision Risk
    Why does that impact matter, which control applies, and what remains?
```

This is also where three often-confused ideas should be separated.

**Risk potential** asks what the consequence could be if a decision condition leads to an unwanted effect. A rule that protects payment idempotency has high risk potential because failure could affect transaction integrity.

**Risk signal** is the observable indication that a concerning condition may be present: missing architecture context, an out-of-scope modification, or a triggered rule that changed the selected alternative.

**Realized engineering effect** is what can actually be demonstrated in the generated document or code: the transaction boundary changed, the public API expanded, or the same idempotency key was preserved.

```text
Risk potential is not a signal
A signal is not proof of harm
An engineering effect is not yet a governance judgment
```

Audit connects these layers. Governance then decides whether to accept, correct, avoid, transfer, or escalate the risk.

Having a risk record does not mean the risk has been governed. Having a control does not mean the risk has been reduced. Both are infrastructure for a repeatable judgment.

The PDCA loop becomes concrete:

```text
Plan: define decision risk conditions, signals, and controls
Do: generate under those controls and capture evidence
Check: compare the condition, control evidence, and resulting effect
Act: accept residual risk or improve the engineering control
```

[[M_EBG_A_06-3.png]]

---

## 6. Example: Controlling Risk in One Payment Retry Decision

Return to the retry decision from Articles 02–05.

The generation received the retry requirement and payment-client code. It produced three alternatives. The idempotency rule triggered and removed the option that created a new key. But the architecture viewpoint for the shared transaction boundary was not supplied, and the generated change also touched that boundary.

The existing RTM links the payment retry requirement to the payment-client design, implementation, and retry tests. VSS also links the client to the shared transaction boundary. Those maintained relationships allow Impact Analysis to extend beyond the edited file without guessing.

The combined analysis and risk record can now stay close to the evidence:

```yaml
decision_risk:
  id: DR-payment-retry-042
  trace_id: TRACE-payment-retry-184
  decision_id: CODE-DEC-042
  generated_artifact: src/payment/client.ts@sha256:...

decision_analysis:
  findings:
    - condition: required architecture context was not supplied
      evidence: FINDING-CONTEXT-001
    - condition: generated effect exceeded approved Change Scope
      evidence: FINDING-SCOPE-002

impact_analysis:
  trace_basis:
    - RTM-payment-requirements@v8
    - VSS-payment-system@v12
  direct_chain:
    - REQ-payment-retry-018@v2
    - DESIGN-payment-client-retry@v5
    - src/payment/client.ts@sha256:...
    - TEST-payment-retry-092
  extended_impact:
    - ref: ARCH-shared-transaction-boundary@v12
      relation: payment client participates in shared transaction handling
    - ref: TEST-payment-duplicate-prevention@v7
      relation: transaction-boundary behavior affects verification coverage

affected_engineering_element:
  ref: VSS-payment-system@v12/system-architecture/transaction-boundary

possible_effect:
  description: >
    Retry logic may change shared transaction semantics without
    an architecture basis visible to the generation.
  risk_potential: high
  rationale: transaction integrity can affect duplicate payment handling

risk_signals:
  - signal: missing-context
    evidence: EVT-context-manifest-104
  - signal: out-of-scope-modification
    evidence: EVT-file-write-212

controls:
  - type: preventive
    action: require the transaction-boundary viewpoint before regeneration
    evidence_expected: context manifest contains the approved viewpoint
  - type: detective
    action: compare generated artifacts with SCOPE-payment-retry@v4
    evidence_expected: scope audit finding
  - type: corrective
    action: revert the shared-boundary change and regenerate
    evidence_expected: corrected diff linked to a new Decision ID

control_result:
  required_context_supplied: true
  out_of_scope_change_removed: true
  evidence:
    - CTX-payment-185@v1
    - FINDING-SCOPE-003
    - DIFF-payment-retry-185

residual_risk:
  condition: original generation cannot be shown to have used architecture context
  treatment: retain as a superseded decision record
  current_change: acceptable-for-review

governance_judgment:
  decision: proceed-to-engineering-review
  basis:
    - risk condition is explicit
    - preventive and corrective controls have evidence
    - residual uncertainty is retained rather than rewritten
```

Notice what the record does not claim.

It does not say the first code change would definitely cause duplicate payments. It says the decision was formed without a required architecture basis and produced an effect outside the approved Scope. That combination creates a visible decision risk.

RTM and Impact Analysis show why the effect cannot be treated as an isolated file edit. The retry requirement traces to the payment client and its tests, while the VSS relationship extends the possible impact to the shared transaction boundary and duplicate-payment verification.

The controls are equally specific. One restores the missing basis. One detects Scope expansion. One removes the unsupported effect and creates a new traceable decision.

The original uncertainty is not erased. The first generation still did not have the architecture context. The corrected generation supersedes it; it does not rewrite its history.

That is the point of engineering-visible decision risk:

> Risk control becomes demonstrable when a visible decision condition is connected to a credible effect, a targeted control, control evidence, and an explicit residual risk.

Engineering makes that chain visible. Governance decides whether the remaining risk is acceptable.

---

## References

- [ISO 31000:2018 Risk Management Guidelines](https://www.iso.org/standard/65694.html)
- [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/)
- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)
- [NIST SP 800-218: Secure Software Development Framework 1.1](https://csrc.nist.gov/pubs/sp/800/218/final)
- [NIST Secure Software Development Framework Project](https://csrc.nist.gov/projects/ssdf)
- [NASA Systems Engineering Handbook: Requirements Management](https://www.nasa.gov/reference/6-2-requirements-management/)
- [NASA Software Engineering Handbook: Bidirectional Traceability](https://swehb.nasa.gov/pages/viewpage.action?pageId=16457931)

### Related Work by the Author

- [Spark Tsai, *Decision Risk: A Structural Governance Framework for AI-Assisted Software Development*](https://doi.org/10.5281/zenodo.19025533)
- [Spark Tsai, *Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development*](https://doi.org/10.31224/6616)
- [Spark Tsai, *Anchor Architecture: A Minimal Structural Foundation for Software Traceability in AI-Assisted Software Development*](https://doi.org/10.31224/6580)
- [Spark Tsai, *Behavior Rule Architecture: Rule-Based Governance of AI System Behavior*](https://doi.org/10.31224/6681)
- [Spark Tsai, *Scope as a Governance Primitive: Making Inference, Authority, Effect, and Evidence Explicit in AI Governance*](https://doi.org/10.5281/zenodo.22108234)
- Spark Tsai, *Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State*, working paper v0.2, 2026.
