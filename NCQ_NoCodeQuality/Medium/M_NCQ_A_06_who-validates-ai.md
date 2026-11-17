# Can AI Use Its Own Tests to Prove It Is Correct?

> When one AI produces the specification, code, tests, and evidence, internal consistency can be mistaken for independent validation.

An AI receives a human request, writes a specification, generates code, creates tests, runs them, and explains why the results show the work is complete. The workflow is fast, coherent, and apparently traceable. It is also capable of becoming a closed self-confirmation loop.

If the AI misunderstood the original intent, every later artifact can inherit the same misunderstanding. Tests can pass because they were derived from the same assumptions as the code. The final evidence can accurately summarize those tests while still failing to demonstrate what the human actually wanted.

The problem is not that AI participated in several steps. The problem is that agreement among artifacts from one reasoning path is treated as independent proof.

---

## Consistency Is Necessary but Not Sufficient

Specification, code, and tests should be consistent. If the specification requires a ten-percent discount and the implementation applies five percent, the mismatch is a clear defect.

But consistency only answers whether the artifacts agree. It does not answer whether their shared premise is correct or complete.

```text
Misunderstood intent
    ↓
Incorrect specification
    ↓
Code consistent with that specification
    ↓
Tests consistent with the same specification
    ↓
Green report
```

Every arrow can be technically correct while the overall result remains wrong for the user.

The same issue occurs with missing risks. If neither the specification nor the generated tests mention duplicate payment, all planned tests can pass without evaluating duplicate payment. A perfect pass rate reveals nothing about a condition absent from the plan.

---

## Independence Has Several Forms

Independent validation does not always require a second human team or a completely separate AI system. Independence can be introduced through different sources, methods, and incentives.

**Source independence** uses information that did not come from the generated specification: original user examples, policy requirements, incident history, contracts, production traces, or domain risk catalogs.

**Method independence** checks the result through a different mechanism: property-based testing, static analysis, security scanning, model checking, exploratory testing, or reconciliation against an external system.

**Actor independence** asks another model, tool, engineer, product owner, or specialist to challenge the result without inheriting every intermediate assumption.

**Decision independence** ensures the system recommending approval is not also authorized to accept the residual risk it identifies.

No single form guarantees correctness. Together they reduce the chance that one hidden premise controls the entire evidence chain.

---

## Start with a Human-Confirmed Intent Baseline

The first independent reference should be a confirmed account of human intent. Before code generation, the AI should restate the problem, expected outcome, boundaries, assumptions, and unresolved choices. The human confirms or corrects that account.

Later evidence should trace back to this baseline, not only to the AI-generated specification. A reviewer should be able to ask whether every critical intent has a corresponding criterion and whether every criterion still represents the confirmed meaning.

This checkpoint does not require the human to design tests or read code. It uses human authority where it is strongest: determining what problem should be solved and which consequences are acceptable.

It also prevents a later specification rewrite from silently changing the goal while keeping the test suite green.

---

## Tests Should Come from Risk as Well as Specification

Tests derived only from the specification tend to reproduce its omissions. A stronger verification plan also derives tests from failure modes and external expectations.

For checkout, risk-derived tests might ask what happens during retry, timeout, concurrency, invalid input, extreme values, insufficient inventory, and partial provider failure. Policy-derived tests might check that sensitive data is not logged. Incident-derived tests might reproduce a past duplicate-order defect.

These tests challenge the implementation from directions that the feature description may not contain.

AI can generate them, but it should disclose their basis. A test linked to a known payment-integrity risk provides different assurance from a test invented because it resembles the code structure. The evidence should preserve that distinction.

---

## A Second AI Is Not Automatically Independent

Using another model can help, but “two AIs agreed” is not a validation design. Models may share training patterns, receive the same incomplete context, or be prompted to confirm rather than challenge.

For a second AI to add value, its role and inputs should differ. It may receive the confirmed intent and risk catalog without seeing the first AI’s tests, then propose adversarial scenarios. It may review evidence specifically for unsupported claims, missing denominators, and unverified environments. It may attempt to falsify the conclusion rather than summarize it.

Disagreement should be preserved for human judgment instead of being averaged into a confident answer. Agreement is useful only when the review paths are sufficiently distinct and their evidence is inspectable.

---

## Evidence Must Expose Its Own Limits

A self-confirming report tends to explain why the work should be trusted. Decision-ready Evidence must also explain why it might not be enough.

It should state which results came from simulation, which environments were used, which cases failed, which were not executed, which risks were not assessed, and which claims depend on assumptions. It should link human-readable statements to technical artifacts so another reviewer can inspect or reproduce them.

For example, “credit-card checkout passed” overstates a simulated-provider test. “The simulated-card path passed; real provider behavior remains unverified” preserves the actual boundary.

An AI should not be permitted to turn missing evidence into positive evidence through fluent explanation.

---

## Separate Recommendation from Authorization

AI can analyze the evidence and recommend that a pull request proceed, be returned, or be escalated. The recommendation should identify the applied criteria, supporting observations, residual risk, and missing information.

Authorization is a separate act. The authorized human or policy mechanism decides whether the evidence is sufficient for a specific transition: merge, deploy, expose to users, or accept risk.

This separation matters most when the AI created the change. The same system can assist every stage, but it should not silently define the requirement, choose the tests, judge their sufficiency, and accept the remaining risk without an external checkpoint.

---

## Validate the Validation Chain

No development process can prove that software contains no unknown defects. The practical goal is to make the validation chain strong enough, diverse enough, and visible enough for the consequence of the decision.

That chain should include a human-confirmed intent baseline, explicit assumptions, criteria from both function and risk, multiple verification methods where needed, visible failures and omissions, traceable evidence, and independent authorization of residual risk.

AI can perform much of the work. It can generate, test, challenge, summarize, and recommend. What it cannot establish through self-consistency alone is that its original understanding was right, its verification plan was complete, or its own evidence is sufficient for the organization’s risk.

No-Code can remove the need for a human to read code. It cannot remove the need for an independently reviewable basis for trust.

---

No-Code Quality · 06 / 06

#NoCodeQuality #AIAssurance #SoftwareTesting #HumanInTheLoop #ArtificialIntelligence
