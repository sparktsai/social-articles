# What Evidence Does a Human Need Without Reading Code?

> A test report becomes useful to a non-coder only when it connects intent, tested behavior, actual results, and unverified risk.

AI can generate code, run tests, and produce a report in seconds. The report may contain coverage percentages, status codes, latency measurements, and a large green number labeled “Passed.” These are useful technical results, but they do not automatically help a human decide whether the change is ready.

A person who cannot review code may still need to approve a pull request. If the evidence says only “42 tests passed,” that person cannot tell whether 42 is the total, whether other tests failed, what users actually did, or what remains unknown.

No-Code development therefore needs more than hidden code. It needs a human-readable quality interface.

---

## Technical Results Are Inputs, Not Decisions

Consider these statements:

- Unit test coverage is 87 percent.
- The checkout endpoint returned HTTP 200.
- P95 latency was 320 milliseconds.
- The regression suite passed.
- No critical exception was detected.

Each statement may be accurate. None tells a product owner whether a customer successfully applied a discount, whether payment created exactly one order, or whether an invalid code trapped the customer in checkout.

The problem is not the terminology alone. Translating “HTTP 200” into “the request succeeded” still does not establish that the intended business result occurred. The response might be successful while inventory is wrong or a confirmation is missing.

Human-readable Evidence must reconstruct the relationship between what the human wanted, what the system did, and what the verification actually observed.

---

## Counts Need Denominators and States

A useful summary should first expose the complete status distribution:

> This verification plan contains 42 test cases: 36 passed, one failed, and five were not executed.

That sentence is more informative than “36 passed,” but counts are still only navigation. The human also needs to know which behaviors occupy each category and how important they are.

Reports should distinguish passed, failed, not executed, blocked, and not applicable. They should not combine “not run” with “passed,” nor hide a critical failure behind a high success percentage. One failed duplicate-charge test can matter more than hundreds of passing display tests.

Severity should be linked to consequence, not merely to how difficult the defect is to fix.

---

## Evidence Should Describe Observable Scenarios

For each material Acceptance Criterion, evidence should show the preconditions, inputs, actions, expected outcome, actual outcome, environment, and result.

A human-readable checkout result might say:

> A customer added two items totaling NT$1,200, applied a valid ten-percent discount, and paid with a simulated credit card. The displayed and stored total became NT$1,080. Payment was approved, one order was created, inventory decreased by one for each item, and a confirmation was produced.

This statement makes the successful path inspectable without exposing code. It also preserves an important limitation: the card was simulated.

A failed result should be equally concrete:

> When the customer entered a discount code that did not exist, checkout stopped responding. The expected validation message did not appear, and the customer could not continue or remove the code.

“Test failed” identifies a status. The scenario explains the user-visible consequence.

---

## Unverified Scope Must Be Visible

The report should also state what was not demonstrated:

- Real credit-card processing was not tested.
- An order total of `99999999999999999999` was not tested.
- Payment interruption and retry behavior were not tested.
- Duplicate submission was not tested.
- Insufficient inventory during payment was not tested.

These statements do not prove defects. They define the boundary of current knowledge.

This is essential because a human may otherwise interpret silence as success. If simulated payment passed and the report simply says “credit-card checkout passed,” the wording extends the evidence beyond what was executed. A precise report says that the simulated integration passed and real payment remains unverified.

Unknown risk should not be converted into a green status merely because no test failed.

---

## Evidence Needs Traceability

Human-readable wording must remain connected to the underlying technical record. Otherwise, AI can produce a persuasive narrative that cannot be checked.

Each claim should link to its Acceptance Criterion, test execution, environment, relevant input, output, timestamp, and artifacts such as screenshots, recordings, logs, or transaction identifiers. The human may not inspect every artifact, but another reviewer or investigator must be able to reproduce the basis of the claim.

Traceability also helps separate interpretation from observation. “The payment experience is reliable” is a conclusion. “Twenty timeout simulations preserved the cart and created no duplicate charge” is evidence that may support part of that conclusion.

The interface should make this distinction visible rather than presenting AI-generated explanations as if they were direct observations.

---

## Human Judgment Is More Than Yes or No

The purpose of Evidence is not to place a human at the end of the pipeline and ask for a yes-or-no click. A human who sees only the AI’s recommendation can approve without understanding what is being accepted. That is a rubber stamp, not meaningful human oversight.

Human-readable Evidence should support a visible reasoning process. After reading the results, the human should be able to consider:

- Which failure or unknown creates a material risk?
- Who or what can be affected, and how widely?
- Is the consequence reversible, detectable, or containable?
- Can the affected function be disabled or restricted?
- Must the issue block the pull request, or can it be tracked for the next sprint?
- Who will own the remaining risk and the follow-up work?

In the checkout example, the human may judge that the invalid-code failure affects every customer using promotions and blocks release. The same human may decide that real-card testing can occur after merge if production activation remains disabled. The decision is not derived from the number of green tests. It comes from understanding the result, estimating impact, considering controls, and choosing a response.

The interface should preserve this judgment: the evidence considered, the risk identified, the chosen treatment, the owner, and any conditions attached to approval. A bare approval records authority but not whether the person actually exercised judgment.

---

## Human-Readable Does Not Mean Simplified Until Harmless

There is a temptation to protect non-technical users from complexity by showing a single score or recommendation. That can remove exactly the information required for judgment.

Human-readable Evidence should reduce unnecessary technical detail, not uncertainty, disagreement, or failure. It should explain consequences in product language while preserving links to technical proof. It should show confidence and limitations rather than manufacture certainty.

The human does not need every log line. The human does need to know that one path failed, five paths were not executed, real payment was not tested, and the AI’s recommendation depends on accepting those facts.

---

## No-Code Needs a Quality Interface

If code disappears but the user receives only coverage, status codes, and green checkmarks, the burden has not been removed. It has moved from unreadable code to an unreadable test report.

A genuine No-Code quality interface connects confirmed intent to Acceptance Criteria, criteria to executed scenarios, scenarios to observed results, and results to residual risk. It lets the human inspect the basis of a delivery decision without pretending that the human has reviewed implementation details.

The purpose is not to guarantee that the software has no defects. It is to make the supported conclusion and its boundary clear: what has been demonstrated, what has failed, what remains unverified, and why a pull request should or should not proceed.

That is the difference between a technical report and decision-ready Evidence.

---

No-Code Quality · 04 / 06

#NoCodeQuality #Evidence #SoftwareTesting #HumanInTheLoop #SoftwareQuality
