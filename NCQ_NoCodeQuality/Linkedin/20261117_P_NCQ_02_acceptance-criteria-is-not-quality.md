# Passing Acceptance Criteria Does Not Prove Software Quality

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

The second problem appeared after AI completed the Acceptance Criteria and I manually tested the result.

The problem was mine, not AI’s.

Almost every Acceptance Criterion described a Happy Path. I had asked whether the expected workflow succeeded, and AI implemented and verified those conditions.

In my previous software work, Happy Paths were usually only about 10–40% of the meaningful conditions I would consider. The rest came from invalid input, boundaries, interruption, retry, failure, recovery, and security.

My No-Code experiment had turned “everything I specified passed” into something that looked dangerously close to “software quality passed.”

For example, a checkout Test may show that a customer added two products totaling NT$1,200, applied a ten-percent discount, paid with a simulated card, and created an order for NT$1,080.

The evidence supports a bounded conclusion:

> This functional path behaved as specified in the tested environment.

It does not show what happens when payment times out, the code is invalid, the customer clicks twice, or inventory changes during payment. Nor does it establish security, performance, recoverability, or data integrity.

Tracing the problem backward revealed the shortcut:

```text
Acceptance Criteria passed
→ Requested function worked in tested examples
→ Software quality passed
```

The final arrow is unsupported unless those additional quality conditions were explicitly identified and verified.

A Human-readable report must distinguish Passed, Failed, Not Executed, and Not Identified. Every planned Test may pass while a material risk was never represented in the plan.

That led directly to my next question: should AI propose the criteria I did not think of?

Software quality is contextual. The Human must judge functional acceptance, relevant quality attributes, residual risk, and the consequence of proceeding.

So the accurate conclusion is not:

> Checkout quality passed.

It is:

> The valid-discount, simulated-card path met its functional Acceptance Criteria. Real payment, invalid-code recovery, interruption handling, and other listed risks remain unverified.

This tells the Human what can be trusted—and where that trust must stop.

**If every Acceptance Criterion passed, what additional Evidence would you still require before calling the software good enough?**

No-Code Quality · 02 / 06

#NoCodeQuality #AcceptanceCriteria #SoftwareQuality
