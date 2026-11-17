# Can a Pull Request Proceed with Failed or Unverified Criteria?

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

Once the report was reconstructed into Human-readable Evidence, another problem became visible.

The normal checkout path worked, but an invalid discount code froze the flow. Simulated-card payment passed, but real-card integration had not been tested.

Human-readable Evidence made the real decision unavoidable: what happens when Evidence contains both success and unresolved risk?

Must every issue be resolved before the pull request proceeds?

A pass percentage was insufficient. “Everything must be perfect” is not practical. “We will fix it next sprint” is not a control.

A failed condition and an unverified condition are also different:

- **Failed:** observed behavior did not match the expectation.
- **Unverified:** the behavior remains unknown.

If the invalid-code Test failed, we know customers can become stuck under those conditions. If real-card payment was not tested, we do not know whether production integration works.

Before accepting either risk, the Human needs to know:

- who and what are affected;
- the worst credible consequence;
- how likely exposure is;
- whether failure can be detected;
- whether it can be contained or reversed;
- what mitigation has been verified;
- who owns the residual risk; and
- when the deferred work must be completed.

Mitigation can change the decision. A defective discount feature might remain disabled behind a verified feature flag. Unverified real payment might block production activation while allowing deployment to a test environment.

This exposes another important distinction:

```text
Open PR
→ Merge
→ Deploy to test
→ Deploy to production
→ Expose to users
```

These are different gates. Approving one transition does not automatically approve the next.

AI can summarize Evidence and recommend block, mitigate, or defer. It should not silently turn a failure into accepted risk. That decision belongs to an authorized Human or an explicit policy-controlled process.

Proceeding does not erase the problem. A deferral must retain its impact, mitigation, owner, tracking item, and escalation point.

“Approved” does not mean quality is complete. It means the Evidence was sufficient for a particular transition under stated conditions.

**What information would allow you to proceed with a failed or unverified condition without allowing it to disappear after approval?**

No-Code Quality · 05 / 06

#NoCodeQuality #RiskAcceptance #SoftwareDelivery
