# Should AI Add the Criteria Humans Did Not Think Of?

> AI should help discover missing risks and hidden requirements, but a suggestion must not silently become an approved product requirement.

Humans usually describe the path they want to succeed. Add a product to the cart, apply a discount, pay, create the order, and send a confirmation. This is a natural way to express intent, but robust software is defined just as much by what happens outside that path.

What if the discount code does not exist? What if payment times out after authorization? What if the customer clicks twice? What if inventory changes between checkout and order creation? What if the order total is larger than the supported numeric range?

AI can recognize many of these patterns. That creates an opportunity for No-Code development: the system can help a human discover conditions that an experienced engineer might normally raise during design or review. It also creates a governance question. When AI proposes more criteria, is it improving verification, changing scope, or inventing requirements?

---

## Missing Criteria Come from Different Sources

Not every missing condition has the same status. Some clarify the behavior already implied by the request. Some represent standard engineering controls. Others are new product choices.

If a customer enters an invalid discount code, showing an error instead of freezing is probably necessary for the stated checkout flow to function. Preventing duplicate charges may be a mandatory safety property of payment processing. Supporting a new payment method, however, is a scope expansion even if AI considers it useful.

Treating all three as equivalent “AI-generated Acceptance Criteria” hides who has authority to decide and why the condition exists.

A better classification is:

- **Confirmed functional criteria:** behavior explicitly accepted by the product owner.
- **Clarification candidates:** conditions needed to make an existing requirement unambiguous.
- **Quality and control conditions:** reliability, security, performance, integrity, accessibility, and recovery expectations derived from risk or organizational standards.
- **Scope suggestions:** potentially useful capabilities that are not required by the current intent.

This separation lets AI contribute without pretending that every plausible idea has already been authorized.

---

## AI Should Show Why It Suggested a Condition

A list of additional tests is not enough. The human needs to understand the reason each item matters.

For every proposed condition, AI should identify the triggering risk, the possible impact, the source of the expectation, and the proposed disposition. A duplicate-payment criterion might be linked to financial loss and data inconsistency. An accessibility condition might come from an organizational standard. A suggestion to add cryptocurrency payment might have no connection to the current risk and should be labeled as a future product option.

The explanation should be concise but decision-oriented:

```text
Suggested condition: repeated submission creates only one charge
Reason: network delay can cause users to click Pay again
Potential impact: duplicate charge and duplicate order
Type: payment integrity control
Recommended disposition: required before release
Approval state: awaiting human confirmation
```

Now the human is not merely accepting AI output. The human can judge whether the risk applies and whether the proposed control belongs in the current change.

---

## Suggestions Need an Explicit State

AI-generated criteria should move through visible states rather than appearing directly in the approved specification.

Useful states include **proposed**, **accepted**, **rejected**, **deferred**, and **required by policy**. The record should identify who changed the state and why. A rejected suggestion should not quietly return in a later generation. A deferred condition should have an owner or tracking item if the risk remains relevant.

This also protects the human from a misleading report. If AI proposes ten risk tests and only the original five functional tests run, the final evidence should not say “all Acceptance Criteria passed.” It should say which approved criteria passed and which proposed or deferred risks remain outside the verified scope.

Visible state prevents suggestion, requirement, test, and result from collapsing into one undifferentiated list.

---

## AI Cannot Know Every Hidden Requirement

AI can draw on common failure patterns, but it does not automatically know the organization’s contracts, operational history, regulatory obligations, support capacity, or risk appetite. It may omit a company-specific control or overemphasize a generic concern.

For example, AI may recommend testing a payment timeout but not know that the business reconciles orders through a separate overnight process. It may suggest a conventional latency target that is irrelevant to an asynchronous workflow. It may fail to identify an accessibility requirement that applies because of the organization’s public-sector customers.

AI suggestions should therefore be treated as risk discovery assistance, not a completeness certificate. “AI found no additional criteria” does not mean no additional risks exist.

Teams can improve coverage by providing relevant context: architectural constraints, incident history, policies, quality standards, supported ranges, and release criticality. They can also maintain reusable risk catalogs for common domains such as identity, payment, privacy, and data migration.

---

## Human Authority Should Focus on Consequences

A non-engineer may not know how to design an idempotency key or simulate a network partition. That should not prevent meaningful review. AI should translate the issue into observable consequences.

Instead of asking whether a particular implementation technique is required, it can ask whether the organization accepts the possibility of two charges when a payment request is repeated. Instead of presenting a database constraint, it can ask whether inventory and order state must remain consistent after partial failure.

The human decides the acceptable outcome and risk. Engineering mechanisms can then be selected and tested against that decision.

This is central to No-Code quality. Human oversight should not require the human to become a software engineer, but it must provide enough information for the human to exercise product and risk authority.

---

## A Practical Review Pattern

Before implementation, AI can produce a compact criteria package:

1. Restate the confirmed intent and functional criteria.
2. Identify ambiguous behavior that needs clarification.
3. Propose quality conditions based on the feature’s risk profile.
4. Separate mandatory organizational controls from optional suggestions.
5. Show potential impact and recommended priority for each addition.
6. Ask the human to accept, reject, defer, or revise each material item.

After implementation, the evidence should preserve those decisions. Accepted conditions should link to results. Deferred conditions should appear as residual risk. Rejected suggestions should remain traceable without being reported as failures.

This process creates more work than immediately generating code, but it moves important decisions to the point where they are cheapest to make and easiest to understand.

---

## AI Expands the Question; Humans Approve the Boundary

AI should not be limited to mechanically testing whatever the human happened to mention. That would preserve every blind spot in the original request. Its ability to suggest edge cases, failure modes, and quality conditions is one of its most valuable contributions.

But discovery is not authority. AI should expand the set of questions, explain why they matter, and make uncertainty visible. Humans and organizational rules should determine which conditions become requirements, which become release gates, and which risks can be deferred.

The objective is neither “AI decides everything” nor “AI only follows instructions.” It is a controlled collaboration: AI searches for what may have been missed; the human confirms intent and accepts consequences; the evidence records both the decision and its limits.

That is how AI can supplement what humans did not think of without quietly redefining what they asked to build.

---

No-Code Quality · 03 / 06

#NoCodeQuality #AcceptanceCriteria #SoftwareRisk #HumanInTheLoop #ArtificialIntelligence
