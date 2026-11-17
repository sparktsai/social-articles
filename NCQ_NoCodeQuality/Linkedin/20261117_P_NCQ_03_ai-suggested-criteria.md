# Should AI Add the Criteria Humans Did Not Think Of?

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

After discovering that nearly all my Acceptance Criteria were Happy Paths, I asked AI to suggest more criteria.

It proposed the kinds of conditions I had missed: an invalid discount code, payment timeout, repeated submission, inventory changing during checkout, and values outside the expected range.

This exposed risks my original request did not cover—and created the next problem.

If AI proposes another Acceptance Criterion, what exactly has happened?

Did it clarify my original Intent, discover a standard engineering control, identify a risk worth testing, or expand the product scope?

The root cause was that “AI-suggested Acceptance Criteria” collapsed different decisions into one label.

When AI proposes another criterion, is it clarifying the requirement, adding a quality control, expanding product scope, or inventing a new requirement?

They should not be treated as one category:

- **Confirmed criteria:** accepted behavior.
- **Clarification candidates:** conditions that remove ambiguity.
- **Quality controls:** expectations derived from risk or policy.
- **Scope suggestions:** possibilities outside the current Intent.

AI should explain why it proposed each condition:

```text
Suggested condition: repeated submission creates only one charge
Reason: users may click Pay again during a network delay
Potential impact: duplicate charge and duplicate order
Type: payment integrity control
Recommended disposition: required before release
State: awaiting Human confirmation
```

The state matters. A suggestion should be **proposed**, **accepted**, **rejected**, **deferred**, or **required by policy**. It should not silently appear as Human-approved.

AI also cannot know every hidden requirement. It may not have the organization’s contracts, incidents, regulations, constraints, or risk appetite.

“AI found no additional criteria” is therefore not a completeness certificate.

The Human need not implement idempotency or simulate a network partition, but must decide whether two charges for one purchase are acceptable.

AI should expand the questions, explain the consequences, and reveal uncertainty. Humans and organizational rules should approve the boundary.

Discovery is not authority.

**When AI discovers a missing condition, is it identifying a risk, proposing a Test, or changing the product requirement—and how should that distinction be recorded?**

No-Code Quality · 03 / 06

#NoCodeQuality #SoftwareRisk #HumanInTheLoop
