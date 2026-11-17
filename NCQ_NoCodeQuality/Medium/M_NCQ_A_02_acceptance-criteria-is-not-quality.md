# Passing Acceptance Criteria Does Not Prove Software Quality

> Acceptance Criteria can show that specified functional behavior was observed. They cannot, by themselves, guarantee the quality of the software that produced it.

In AI-assisted development, a green list of Acceptance Criteria can feel like a complete answer. The human described a feature, the AI implemented it, and every listed criterion passed. If the human does not read code, this may appear to be the strongest available reason to approve the change.

It is an important reason, but it is not a complete quality judgment.

Acceptance Criteria and software quality answer different questions. Confusing them creates a dangerous shortcut: “the requested function worked in the tested examples” becomes “the software is good enough to release.” The first statement may be supported by evidence while the second remains largely untested.

---

## What Acceptance Criteria Actually Establish

Acceptance Criteria translate a requirement into observable conditions. For a checkout change, a criterion might state:

> Given two products totaling NT$1,200, when the customer applies a valid ten-percent discount code and pays by credit card, then the order total is NT$1,080, payment succeeds, an order is created, inventory is reduced, and a confirmation is sent.

If the test reproduces those conditions and observes those outcomes, the evidence supports a bounded conclusion: this functional path behaved as specified in the tested environment.

The limitation is in the boundary. The criterion says nothing about inputs, environments, timing, failure modes, or quality attributes that it did not include.

---

## A Green Functional Path Leaves Many Questions Open

The successful checkout example does not automatically tell us what happens when the discount code does not exist, expires during checkout, or is applied twice. It does not show whether a repeated click causes two payment requests, whether inventory remains correct after a timeout, or whether an order can be recovered after a partial failure.

It may use a simulated card rather than the production payment provider. It may run with a small database and one user rather than production traffic. It may never test an order total of `99999999999999999999`, malformed text, unusual currencies, or a boundary between time zones.

The feature can satisfy its stated Acceptance Criteria while still being slow, insecure, inaccessible, difficult to operate, or fragile under failure.

These are not obscure objections to an otherwise successful test. They are different dimensions of software quality:

- **Reliability:** does behavior remain correct across failures and retries?
- **Security:** can unauthorized input or access change the outcome?
- **Performance:** does the system respond within acceptable limits under realistic load?
- **Data integrity:** can money, inventory, and order state become inconsistent?
- **Recoverability:** can the system return to a safe state after interruption?
- **Usability and accessibility:** can intended users understand and complete the flow?
- **Operability:** can the team detect, diagnose, and control failures in production?

A functional criterion may include one of these properties, but it does not cover them merely because it is an Acceptance Criterion.

---

## Quality Needs Explicit Conditions and Evidence

The answer is not to stretch every Acceptance Criterion until it contains every possible quality concern. That would make criteria unreadable and still fail to guarantee completeness.

A better approach is to preserve the distinction between functional acceptance and quality evaluation. Functional Acceptance Criteria describe the behavior required by the feature. Quality conditions describe the levels, constraints, failure behavior, and controls required for the software to be acceptable in its context.

For the checkout example, additional quality conditions might require that duplicate payment submissions are idempotent, payment-provider timeouts do not lose the cart, order totals cannot overflow supported numeric ranges, sensitive card data never enters application logs, and the service meets a defined latency target under a specified load.

Each condition needs its own evidence. A unit test cannot prove production payment integration. A simulated provider can verify request handling but not the behavior of a real acquiring network. A single response-time measurement cannot establish performance under sustained load.

Evidence must therefore state not only the result, but also the environment, input, preconditions, scope, and limitations of the test.

---

## “Not Tested” Is Different from “Passed”

Human-readable reporting must distinguish at least four states:

- **Passed:** the condition was executed and the observed result matched the expectation.
- **Failed:** the condition was executed and the observed result did not match.
- **Not executed:** the team knows the condition exists but did not run it.
- **Not identified:** the risk or condition was never represented in the verification plan.

The fourth state is especially important. A report can show that every planned test passed while the plan itself omitted a material risk. Green results do not reveal what nobody thought to test.

AI can help scan for missing conditions, but its suggestions must remain visible as suggestions rather than silently becoming approved requirements. Human owners still need to decide which risks apply, what level is acceptable, and what must block delivery.

---

## Quality Is a Judgment, Not a Single Test Status

Software quality is contextual. The evidence required for a personal note-taking tool is different from the evidence required for a payment system, medical workflow, or identity service. There is no universal set of Acceptance Criteria that guarantees quality for every product.

A delivery decision combines several judgments:

```text
Functional acceptance
    Did the required behavior work?

Quality evaluation
    Were relevant quality attributes tested to acceptable levels?

Residual risk
    What failed, was omitted, or remains unverified?

Delivery decision
    Is that residual risk acceptable for this release and context?
```

Acceptance Criteria contribute to the first judgment. They may contribute to the second when quality properties are explicitly included. They do not eliminate the third or make the fourth automatically safe.

This distinction also improves discussion. Instead of arguing whether a feature is simply “done,” a team can say that functional acceptance is complete, real-card integration remains unverified, the invalid-code path fails, and the release owner must decide whether those facts block the pull request.

---

## No-Code Makes the Boundary More Important

When a human can review code, architecture, and test design, that reviewer may notice missing controls or questionable assumptions. In a No-Code workflow, the human may see only specifications, Acceptance Criteria, and generated evidence. If the interface presents a row of green criteria as “quality passed,” the human is being asked to make a broader judgment than the evidence supports.

The system should instead show exactly what each result proves. It should connect every criterion to its executed scenario, expected outcome, actual outcome, and test environment. It should separately present failed conditions, unexecuted conditions, known exclusions, and quality risks that were not assessed.

That is not pessimistic reporting. It is the information required for meaningful human control.

---

## Use the Narrowest Supported Conclusion

The correct conclusion from the checkout example is not “the checkout software has good quality.” It is:

> The valid-discount, simulated-card path met its specified functional Acceptance Criteria in the test environment. Real payment integration, invalid-code recovery, extreme values, interruption handling, and other listed quality risks remain failed or unverified.

This statement may sound less impressive than “all tests passed,” but it is more useful. It tells the human what can be trusted, where that trust stops, and what decision remains.

Acceptance Criteria are essential because they turn requirements into observable behavior. Their value is weakened, not strengthened, when they are asked to serve as a guarantee they cannot provide.

In No-Code software development, quality depends on maintaining the boundary: functional acceptance proves specified behavior within tested conditions; software quality requires broader evidence, explicit risk evaluation, and a human decision about what remains unknown.

---

No-Code Quality · 02 / 06

#NoCodeQuality #AcceptanceCriteria #SoftwareQuality #SoftwareTesting #HumanInTheLoop
