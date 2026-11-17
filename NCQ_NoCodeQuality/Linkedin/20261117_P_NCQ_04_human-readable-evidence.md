# What Evidence Does a Human Need Without Reading Code?

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

The fourth problem appeared when I received the Test Report.

The report gave me numbers, but not enough meaning to judge the software. I was being pushed back toward reading the Code—the exact thing this experiment excluded.

So I asked AI to explain the results.

That created a second risk: the explanation could become an inference from numbers rather than Evidence of observed behavior. It could sound convincing without demonstrating what actually happened.

For example, AI can report:

- Unit test coverage: 87%.
- HTTP status: 200.
- Regression suite: passed.
- 36 Tests passed.

These results may be accurate. They do not show what the user did, what the system produced, or what remains unknown.

Translating “HTTP 200” into “the request succeeded” does not solve the problem. The request may succeed while inventory is wrong or confirmation is missing.

Human-readable Evidence must reconstruct the relationship between Intent, expected behavior, actual behavior, and unverified risk.

Instead of only saying:

> Checkout E2E Test passed.

The Evidence could say:

> A customer added two products totaling NT$1,200, applied a ten-percent discount, and paid with a simulated card. The order total became NT$1,080. One order was created, inventory decreased, and a confirmation was produced.
>
> Real-card processing, payment interruption, duplicate submission, and insufficient inventory were not verified.

Now the Human can compare what was expected with what was observed—and see where current knowledge ends.

Counts need denominators: “36 passed” is less useful than “42 planned: 36 passed, one failed, five not executed.”

Human-readable does not mean simplifying until uncertainty disappears. It means removing unnecessary technical detail while preserving failures, disagreement, assumptions, and limitations.

Every claim must remain traceable to its Acceptance Criterion, execution, environment, inputs, outputs, and artifacts. Otherwise, AI can turn numbers into a persuasive story nobody can verify.

If Code disappears but the Human receives only green checkmarks and technical metrics, the burden has not disappeared. It has moved from unreadable Code to an unreadable Test Report.

No-Code needs a Human-readable quality interface.

**If you could not read the Code, what would AI have to show you before you were willing to merge the pull request?**

No-Code Quality · 04 / 06

#NoCodeQuality #Evidence #SoftwareTesting
