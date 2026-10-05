# Your AI Change Is "High Risk." What Exactly Should You Control?

**Engineering Before Governance | 06 / 08**

A payment change is marked high risk. The team adds another approval.

What if the underlying condition is missing architecture context? Or an unauthorized change to a transaction boundary? Or a rule whose delivery cannot be established?

Those conditions need different treatments. A risk score helps prioritize attention; effective control requires a more specific starting point.

[[L_EBG_A_06-0.png]]

## Translate the rating into an observable condition

Risk registers, matrices, threat modeling, review gates, tests, and security analysis all contribute to risk management. The challenge here is to connect a concern to one AI-assisted development decision.

"Payment integrity risk" does not tell an engineer what to fix. A useful record might instead say:

> The retry decision has no supported delivery record for the required architecture viewpoint, and the generated diff modifies a shared transaction boundary outside approved Scope.

That statement names the evidence gap and the observed effect. It gives analysis and treatment a concrete subject.

The code may still pass focused tests. That leaves a separate question about its basis, authorization, and wider impact. Conversely, a defect with clear provenance and effective correction does not automatically establish a decision-governance failure.

## Use three analyses for three questions

[[L_EBG_A_06-1.png]]

**Decision Analysis** compares the generated effect with the approved Scope. What changed? Did an unsupported or unauthorized effect appear? Can that effect be traced to the recorded decision basis?

**Impact Analysis** follows the affected engineering chain. A Requirements Traceability Matrix (RTM) connects requirements to design, code, tests, and verification. System-view and dependency relationships can extend the analysis to interfaces and architecture boundaries.

**Decision Risk** interprets those findings. Why could the condition matter, which control addresses it, and what uncertainty remains afterward?

An RTM link establishes a maintained relationship. It does not prove the requirement entered the model's context or that every linked component changed. Development Evidence and impact tracing answer complementary questions.

The resulting chain is:

```text
Observed decision condition
    -> generated effect relative to Scope
    -> affected requirements, designs, code, and tests
    -> credible consequence
    -> targeted control
    -> control evidence and residual risk
    -> authorized judgment
```

## Match the control to the condition

[[L_EBG_A_06-3.png]]

For the payment retry example, suppose the generated diff crosses the approved transaction boundary and required architecture delivery is unproven.

A **preventive** control requires the approved transaction-boundary viewpoint before a new generation and captures its delivery.

A **detective** control compares the generated effect with the approved Scope and checks relevant structural relationships.

A **corrective** control removes the unsupported modification and produces a new traceable decision under the corrected basis.

Each control needs an expected result and supporting evidence. "Reviewed" is too broad to establish whether the condition was addressed.

After correction, a manifest may establish delivery of the required viewpoint. A new scope finding may establish that the unexpected change was removed. Relevant tests can provide additional artifact verification.

Those records support a claim about treatment of the identified condition. They do not guarantee the absence of every future payment failure.

[[L_EBG_A_06-2.png]]

## Keep potential, signals, and effects distinct

Transaction integrity creates serious **risk potential**. Missing context is a **risk signal**. A demonstrated transaction-boundary modification is a **realized engineering effect**.

A signal can justify investigation without proving harm. An engineering effect needs interpretation against requirements and authority before it becomes a governance judgment.

Likewise, the absence of a captured signal may reflect limited instrumentation. If rule-trigger events were never recorded, an empty trigger list does not establish that no rule triggered.

Clear evidence limits help avoid both exaggeration and false reassurance.

## Close the risk with evidence of what remains

The original generation cannot be rewritten to look as though it received missing context. Retain its limitation and link the corrected generation as a successor.

Record what the control changed, what evidence supports that result, and what residual uncertainty remains. Then identify the role authorized to accept, return, or escalate the remaining risk.

The next time a change receives a high-risk label, ask for its observable condition, credible effect, targeted control, and closure evidence. That turns a prioritization signal into work the engineering team can actually perform and review.

## Further Reading

- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)
- [NASA: Requirements Management](https://www.nasa.gov/reference/6-2-requirements-management/)
- [Spark Tsai: Decision Risk](https://doi.org/10.5281/zenodo.19025533)
- [Spark Tsai: Decision Analysis](https://doi.org/10.31224/6616)

#EngineeringBeforeGovernance #DecisionRisk #AIGovernance #SoftwareEngineering
