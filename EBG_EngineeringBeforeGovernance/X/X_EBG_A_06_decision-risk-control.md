# Your AI Change Is “High Risk.” What Exactly Should You Control?

**Engineering Before Governance — Main Series 06 / 08**

[[X_EBG_A_06-0.png]]

A payment change is marked high risk. The team adds another approval.

But what if the underlying condition is missing architecture context? An unauthorized transaction-boundary change? Or a rule whose delivery cannot be established?

Those conditions need different treatments. A score can prioritize attention. Effective control requires a more specific starting point.

## Translate a rating into an observable condition

Risk registers, matrices, threat modeling, review gates, tests, and security analysis all contribute to risk management. The challenge is connecting the concern to one AI-assisted development decision.

“Payment integrity risk” does not tell an engineer what to fix. A useful record might say:

> The retry decision has no supported delivery record for the required architecture viewpoint, and the generated diff modifies a shared transaction boundary outside approved scope.

That statement names an evidence gap and an observed effect. It gives analysis and treatment a concrete subject.

The code may still pass focused tests. That leaves a separate question about its basis, authorization, and wider impact. Conversely, a defect with clear provenance and effective correction does not automatically prove a governance failure.

## Use three analyses for three questions

**Decision Analysis** compares the generated effect with approved scope. What changed? Did an unsupported or unauthorized effect appear? Can it be traced to the recorded decision basis?

**Impact Analysis** follows the affected engineering chain. A Requirements Traceability Matrix can connect requirements to design, code, tests, and verification. Dependency relationships extend the analysis to interfaces and architecture boundaries.

**Decision Risk** interprets those findings. Why could the condition matter, which control addresses it, and what uncertainty remains afterward?

An RTM link establishes a maintained relationship. It does not prove that a requirement entered model context or that every linked component changed. Development evidence and impact tracing answer complementary questions.

The useful chain is:

```text
Observed condition
  -> effect relative to scope
  -> affected engineering elements
  -> credible consequence
  -> targeted control
  -> control evidence and residual risk
  -> authorized judgment
```

## Match the control to the condition

Suppose a generated diff crosses the approved transaction boundary and required architecture delivery is unproven.

A **preventive control** requires the approved architecture viewpoint before a new generation and captures its delivery.

A **detective control** compares the generated effect with scope and checks relevant structural relationships.

A **corrective control** removes the unsupported modification and creates a new traceable decision under the corrected basis.

Each control needs an expected result and supporting evidence. “Reviewed” is too broad to show whether the condition was addressed.

After correction, a manifest may establish delivery of the required viewpoint. A new scope finding may establish that the unexpected edit was removed. Tests can add artifact verification.

Those records support treatment of the identified condition. They do not guarantee the absence of every future payment failure.

## Keep potential, signal, and effect separate

Transaction integrity creates serious **risk potential**. Missing context is a **risk signal**. A demonstrated boundary modification is a **realized engineering effect**.

A signal can justify investigation without proving harm. An effect needs interpretation against requirements and authority before becoming a governance judgment.

Likewise, an empty event list may reflect limited instrumentation. If rule triggers were never recorded, no captured trigger does not mean no rule triggered.

Close the risk by recording what the control changed, what evidence supports the result, what uncertainty remains, and who may accept or escalate it.

The next time a change receives a high-risk label, can the team name its observable condition, targeted control, and closure evidence?

## Sources

- [NIST AI RMF Playbook](https://airc.nist.gov/airmf-resources/playbook/)
- [NASA: Requirements Management](https://www.nasa.gov/reference/6-2-requirements-management/)
- [Decision Risk](https://doi.org/10.5281/zenodo.19025533)
- [Decision Analysis](https://doi.org/10.31224/6616)

#EngineeringBeforeGovernance #DecisionRisk #AIGovernance #SoftwareEngineering
