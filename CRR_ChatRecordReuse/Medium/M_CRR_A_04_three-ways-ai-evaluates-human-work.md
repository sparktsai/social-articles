# Three Ways AI Evaluates or Challenges Human Work

![AI and Human work through critique review and dialectic](illustrations/M_CRR_A_04.png)

> “Give me feedback” can mean at least three different things: evaluate this, inspect this, or challenge this.

AI is frequently asked to respond to work that already exists.

Review this draft.

Tell me what is wrong.

Challenge my argument.

These requests are often grouped together as feedback. But they establish different relationships between Human and AI, produce different records, and require different next steps.

The three forms are **Critique, Review, and Dialectic**.

- Critique evaluates qualities.
- Review checks against expectations.
- Dialectic tests a claim through opposition.

Confusing them can produce the wrong kind of output. A critique may sound insightful but fail to identify requirement violations. A review may find defects but say little about the strength of the underlying argument. A dialectical challenge may improve a claim even when no formal defect exists.

---

## 1. Critique: AI as Critic

In critique, the Human presents an idea, artifact, or position. AI evaluates it from a specified or inferred perspective.

The focus is qualitative.

AI may discuss:

- clarity;
- coherence;
- persuasiveness;
- strengths and weaknesses;
- audience fit;
- tone;
- originality of framing;
- or alternative interpretations.

Critique is valuable when the Human wants to understand how the work may be perceived or where it could become stronger.

But critique depends on criteria.

“Is this good?” is weak because “good” has no defined reader, purpose, or standard. The response may reflect generic preferences rather than the intended use.

A better critique request identifies the lens:

> Critique this product description for a developer who already uses Codex and believes manual copy-and-paste is sufficient.

Now the response can reveal a concrete positioning problem.

A critique record is reusable when it preserves:

- the evaluation criteria;
- the intended audience;
- strengths worth retaining;
- weaknesses worth considering;
- and which suggestions the Human accepted or rejected.

The output can become a revision plan or a comparison of how different audiences respond.

---

## 2. Review: AI as Inspector

Review is more constrained.

The Human presents an artifact and expects AI to check it against requirements, standards, rules, or acceptance conditions.

Typical review questions include:

- Is every required section present?
- Does this change stay within scope?
- Are the claims supported?
- Does the implementation match the specification?
- Does the document violate any stated rule?

Useful review content includes:

- the standard or requirement used;
- the reviewed scope;
- each identified problem;
- severity or impact;
- the required correction;
- unresolved questions;
- and the status after correction.

This is different from critique.

A sentence may be stylistically weak but still satisfy every requirement. That is a critique concern, not necessarily a review failure.

Another sentence may be elegant but make an unsupported product claim. That is a review problem even if the writing is strong.

A reusable review record should be transformable into action:

```text
Finding
→ affected artifact
→ applicable requirement
→ requested correction
→ status
→ verification result
```

That structure can move into an issue tracker or checklist while the full topic record preserves the surrounding conversation.

---

## 3. Dialectic: AI as Opponent

Dialectic is not primarily about evaluating an artifact or checking compliance.

It is about testing a claim.

The Human proposes a position. AI is asked to challenge it, produce counterexamples, expose hidden assumptions, or defend an opposing view. The Human responds, narrows the claim, changes a condition, or rejects the challenge.

The value comes from the exchange.

A dialectical conversation can produce:

- counterarguments;
- counterexamples;
- hidden premises;
- boundary cases;
- conditions under which the claim fails;
- and a revised claim that can survive stronger scrutiny.

Suppose the initial claim is:

> Recording AI conversations creates reusable knowledge.

A dialectical challenge may ask:

- What if the conversation contains incorrect information?
- What if the transcript is too long to reuse?
- What if recording adds more organization work than it saves?
- What if native search already solves the problem?
- What exactly becomes knowledge rather than merely stored text?

Those questions do not simply “criticize the writing.” They force the claim to become more precise:

> Recording preserves reusable working material when the topic has future value, the relevant range is selected, important claims are verified, and downstream tools transform the record into an appropriate artifact.

That is a stronger, more bounded claim.

---

## The Same Artifact Can Need All Three

Consider a Capafy product detail page.

It may need **critique** to determine whether the value proposition is clear to the intended buyer.

It may need **review** to check whether every described capability actually exists and whether limitations are disclosed.

It may need **dialectic** to challenge the premise that a paid recorder provides enough value when users can manually copy a transcript.

```text
Critique
→ Is it clear and persuasive?

Review
→ Is it accurate and compliant with stated requirements?

Dialectic
→ Does the underlying claim survive opposition?
```

These are complementary, not interchangeable.

---

## Revision and Verification Are Activities, Not Always New Forms

Critique, review, and dialectic often lead to revision.

Review and dialectic may also require verification.

But revision and verification can occur across several conversation forms. A learning conversation may verify an example. A creative conversation may revise a draft. An assistance conversation may verify a source.

It is often more useful to treat them as second-layer activities:

```text
Primary form: Review
Activity: Verification

Primary form: Creation
Activity: Revision
```

This keeps the main relationship clear while still recording what happened.

---

## Ask for the Kind of Feedback You Need

Before asking AI to “review” something, decide what role it should play.

Do you want an audience-aware evaluation?

Do you want a requirements-based inspection?

Or do you want an opponent that tries to break the claim?

The answer changes the prompt, the output, and the way the record should be reused.

“AI gave feedback” is not enough.

The useful question is:

> **Was it a critique, a review, or a challenge—and what decision followed?**

Chat Record Reuse · 04 / 10

#ArtificialIntelligence #CriticalThinking #QualityAssurance #Writing #AIGovernance
