# Can a Pull Request Proceed with Failed or Unverified Criteria?

> A failed test does not always block delivery, but deferring it requires an explicit risk decision, not a promise to fix it later.

Software delivery rarely reaches a state in which every possible condition has been tested. A No-Code workflow changes who must understand the remaining uncertainty and how it must be presented.

Suppose the normal checkout path works, but an invalid discount code freezes the flow. Simulated card payment passes, but real-card integration has not been tested. Should the pull request wait until every issue is resolved, or can the team merge now and schedule the remaining work for the next sprint?

The answer cannot come from the pass rate alone. It requires a structured judgment about consequence, exposure, control, and responsibility.

---

## “Not Perfect” Is Not a Decision Rule

Requiring perfection would stop most delivery. Accepting every known issue would make testing meaningless. Teams need a boundary between conditions that must block progress and conditions that can be accepted temporarily.

That boundary should not be based only on whether an item is labeled an Acceptance Criterion. A failed cosmetic criterion may be tolerable for an internal preview. An untested duplicate-payment condition may be unacceptable even if nobody wrote it into the original criteria.

The important question is what can happen if the change proceeds.

A Blocking Issue usually involves an unacceptable consequence, such as financial loss, security exposure, corrupted or unrecoverable data, regulatory violation, loss of a critical workflow, or a failure that cannot be safely detected and contained. The exact boundary depends on the product and release context, but the decision must be connected to impact.

---

## Failure and Missing Evidence Are Different

A failed condition provides evidence that observed behavior did not match the expectation. An unverified condition means the behavior remains unknown. Both can create risk, but they support different claims.

If the invalid discount-code test failed, the team knows customers can become stuck under the tested conditions. If real-card payment was not tested, the team does not know whether production integration works. It would be misleading to describe both as “pending tests” or to treat the untested integration as less serious merely because it has not produced a red result.

The review package should distinguish:

- failed criteria and their observed consequences;
- tests that were planned but not executed;
- risks that were identified but have no test yet;
- conditions outside the current scope;
- assumptions that remain unsupported.

This prevents absence of evidence from being interpreted as evidence of success.

---

## A Deferral Needs Decision-Ready Information

Before a human accepts a failure or gap, the evidence should answer several questions.

**Who and what are affected?** Does the issue affect all users, a rare input, an internal operator, or a critical customer segment?

**What is the worst credible consequence?** Can it cause inconvenience, lost work, financial harm, data inconsistency, security exposure, or legal obligations?

**How likely is exposure?** Is the path impossible in the release configuration, uncommon but available, or part of normal use?

**Can the problem be detected?** Will monitoring or support know that it occurred, or can it remain silent?

**Can the effect be contained or reversed?** Is there a feature flag, rollback, manual recovery process, or safe fallback?

**Who owns the residual risk?** Which authorized person accepts it, and which person is responsible for correction?

**When will it be resolved?** Is there a tracked item, target release, and condition for escalation?

Without these answers, “next sprint” is not a control. It is only an optimistic statement about the future.

---

## Mitigation Can Change the Decision

The same defect can support different decisions depending on release controls.

If invalid discount codes freeze checkout for every customer, the issue may block release. If the discount feature can remain disabled behind a feature flag while the rest of the change is merged, the pull request may proceed without exposing users. If real payment is unverified, a sandbox-only deployment may be acceptable while production activation remains blocked.

Mitigation must be real and testable. A feature flag should be shown to prevent access. A rollback procedure should have an owner and usable artifact. Monitoring should detect the specific failure rather than merely report that the service is online.

The evidence should describe the mitigated state that is being approved. Approval to merge code is not automatically approval to enable the feature in production.

---

## Pull Request, Deployment, and Release Are Separate Gates

Teams often use “Can we PR?” as shorthand for several decisions. A pull request may be opened, approved, merged, deployed to a test environment, deployed to production, or exposed to users. Each transition can have a different risk threshold.

A team might merge incomplete work behind a disabled flag, deploy it to staging for real-provider testing, and block production activation until evidence is complete. Collapsing these stages into one yes-or-no status creates unnecessary conflict: either all incomplete work is forbidden, or risky behavior is released too early.

A No-Code quality interface should identify the requested decision. The human needs to know whether they are authorizing code integration, environment deployment, user exposure, or risk acceptance for full release.

This also clarifies responsibility. An engineer may approve technical integration while a product or risk owner decides whether a known limitation is acceptable to users.

---

## Deferred Work Must Remain Connected

Once a pull request proceeds, deferred items easily disappear into a backlog. The decision record should preserve a connection between the accepted risk and the follow-up work.

At minimum, it should include the failed or unverified condition, impact, mitigation, owner, tracking identifier, due date or target release, and the event that requires escalation. If the risk changes, the record should be updated rather than overwritten.

The next review should be able to ask whether the promised control remained active and whether the deferred condition was completed. Otherwise, repeated acceptance can turn a temporary exception into an undocumented permanent state.

---

## AI Can Recommend, but It Should Not Accept Risk

AI can summarize failures, estimate affected paths, compare them with organizational rules, and recommend block, mitigate, or defer. It can also identify missing information that prevents a decision.

But AI should not silently convert a failed criterion into an accepted risk. Acceptance belongs to an authorized human or policy-controlled process because it commits the organization to a consequence.

The recommendation should therefore separate facts from judgment:

```text
Observed: invalid discount code blocks checkout
Exposure: available to all customers using promotions
Impact: checkout cannot continue
Mitigation: none currently verified
Recommendation: block user release
Decision: awaiting authorized human
```

This makes oversight meaningful even when the human cannot read code.

---

## Proceeding Does Not Mean the Problem Disappeared

The strongest outcome is not always “fix everything before merge.” It is a decision whose evidence matches its scope.

A pull request can proceed with a known issue when the consequence is understood, exposure is controlled, mitigation is verified, responsibility is assigned, follow-up is traceable, and an authorized person explicitly accepts the residual risk. It should not proceed when the potential consequence is unacceptable, the behavior is critical and unknown, or the proposed control exists only as an assertion.

“Approved” therefore does not mean “quality is complete.” It means the evidence was sufficient for a particular transition under stated conditions.

No-Code software development needs this precision because the approving human cannot compensate by inspecting implementation details. The system must show what failed, what remains unknown, what control exists, and what obligation continues after approval.

That is how a team can defer work without deferring accountability.

---

No-Code Quality · 05 / 06

#NoCodeQuality #PullRequest #RiskAcceptance #SoftwareDelivery #HumanInTheLoop
