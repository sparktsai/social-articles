# Can AI Use Its Own Tests to Prove It Is Correct?

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

The sixth problem appeared just before the pull request.

I found that there was no Test Code.

AI had reported verification results, but there was no executable Test artifact I could rerun in an isolated sandbox. The Evidence depended on the same process that produced the implementation.

This was not independent sandbox testing. It was AI generating the implementation, checking the result through its own path, and then explaining why that result should be trusted.

Tracing backward revealed a self-confirmation loop: one AI interpreted the request, wrote the Specification and Code, chose the verification, and explained why it passed.

```text
Misunderstood Intent
→ Incorrect Specification
→ Code consistent with that Specification
→ Tests consistent with the same Specification
→ Green Report
```

Every artifact can agree while the overall result remains wrong for the Human.

The absence of Test Code made the distinction concrete: consistency is necessary, but it is not reproducible or independent validation.

Independence can come from different directions:

- **Source:** user examples, policies, incidents, contracts, or risk catalogs.
- **Method:** static analysis, security scans, property-based or exploratory testing.
- **Actor:** another tool, model, specialist, or Human challenges the result.
- **Decision:** the system recommending approval does not accept the risk.

A second AI is not automatically independent. Two models may receive the same incomplete context or be prompted to confirm rather than challenge.

A second AI adds more value with different inputs and an objective to falsify the conclusion rather than confirm it.

Tests should come from risk as well as the Specification. Retry, timeout, concurrency, privacy rules, and past incidents can expose inherited omissions.

Evidence must expose simulated providers, failed and unexecuted cases, unassessed risks, boundaries, and assumptions.

AI can generate, test, challenge, summarize, and recommend. Self-consistency alone cannot prove that its original understanding was right or its verification plan complete.

No-Code may remove the need for a Human to read Code. It cannot remove the need for an independently reviewable basis for trust.

**When AI produces both the implementation and the Evidence supporting it, what would count as sufficiently independent validation?**

No-Code Quality · 06 / 06

#NoCodeQuality #AIAssurance #HumanInTheLoop
