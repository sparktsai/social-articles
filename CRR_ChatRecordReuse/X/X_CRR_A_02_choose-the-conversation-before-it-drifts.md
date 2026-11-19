# Choose the Conversation Before It Drifts

![Human keeps an AI conversation aligned while preserving useful branches](X_CRR_A_02.png)

You ask AI to verify one claim.

Several replies later, you are discussing product strategy.

You ask for a review against requirements. AI rewrites the document.

You ask to compare three options. AI opens five new research directions, and the original decision disappears.

The detour may be useful.

The problem is that the purpose changed without an explicit decision.

## AI Can Always Continue

Conversational AI can offer another framework, question, risk, improvement, or adjacent problem.

That is valuable in Exploration.

It can be harmful in a bounded Inquiry, a requirements-based Review, or a decision that must converge.

This is not about AI intending to take control. It is about the conversation having no visible boundary.

When the Human supplies only a prompt, plausible continuation can become direction-setting.

## Begin with a Conversation Contract

Before a substantial AI conversation, define six things.

### Topic

What continuing subject does this work belong to?

Name the work, not the chat session.

### Mode

What kind of conversation do you need?

Inquiry, Learning, Advisory, Assistance, Discussion, Exploration, Analysis, Creation, Critique, Review, Dialectic, or Reflection?

### Purpose

Why are you having this conversation?

“Discuss this” provides little direction.

“Identify which assumptions make this recommendation unsafe” does.

### Output

What should exist at the end?

A direct answer? A comparison? A decision? Review findings? A revised claim? A draft?

### Boundary

What is outside this conversation?

Name the topics, files, decisions, audiences, or changes that should not be handled now.

### Stop Condition

When should the conversation converge, stop, or open a new Topic?

Without a stop condition, every answer can create another plausible task.

## Different Modes Need Different Instructions

Inquiry should remain bounded:

```text
Answer this question.
Identify missing information.
Do not expand into implementation advice.
```

Exploration should diverge intentionally:

```text
Explore possible problem definitions.
Do not converge early.
Group the branches at the end.
```

Analysis should expose its basis:

```text
Use these criteria.
Separate facts, assumptions, missing evidence,
and conclusions.
```

Review should follow explicit standards:

```text
Review against these requirements.
Report findings and affected sections.
Do not rewrite the artifact.
```

Dialectic should challenge:

```text
Give the strongest counterexamples.
Identify the conditions under which this claim fails.
```

The prompt does more than request content. It assigns a relationship between Human and AI.

## A Common Drift Pattern

Suppose the task is to verify one sentence in a product description.

The intended contract is:

```text
Topic: Product claim verification
Mode: Assistance
Purpose: Check the evidence for one sentence
Output: Supported, unsupported, or qualified
Boundary: Do not rewrite positioning
Stop: Evidence is found or remains unresolved
```

AI cannot find decisive evidence, but offers a stronger way to describe the product. The Human asks for an example. AI rewrites the paragraph, proposes a new audience, and compares competitors.

The replies may be useful. Yet the interaction moved from Assistance to Creation and then toward Advisory. The original claim remains unverified.

Fluency makes the movement feel like progress. The contract shows that it is another task.

The Human can return to verification, accept that the claim is unresolved, or open a separate Topic for positioning. A valuable detour should not masquerade as completion.

## Notice Mode Changes

Useful conversations often change mode.

Learning reveals a decision. Analysis uncovers a question that needs Exploration. Critique leads to Creation. Review leads to Reflection.

Switching is allowed.

Switching without noticing is the problem.

When AI introduces a valuable new direction, the Human can:

1. keep the current mode and place it in a backlog;
2. explicitly switch modes;
3. preserve the current work and open a separate Topic.

A one-line note is enough:

```text
Mode change: Analysis → Exploration
Reason: The evidence exposed three unresolved problem definitions.
```

This prevents exploratory ideas from later looking like analytical findings.

## Use an Alignment Checkpoint

After several replies—or when a major new direction appears—ask:

```text
Are we still working on the same Topic?
Are we still using the intended Mode?
Does this support the original Purpose?
Is the expected Output still the same?
Should this branch move to a backlog or separate Topic?
```

Use checkpoints where drift is costly: consequential decisions, requirements, published claims, research, or work that will be handed to someone else.

## Make Handoffs Interpretable

A conversation contract also helps teams.

Without it, a colleague must infer whether AI was brainstorming, recommending, checking, or producing approved content.

With it, they can interpret the record correctly:

- Exploration contains possibilities, not commitments.
- Advisory contains recommendations, not decisions.
- Review findings should point to requirements.
- Creation may include rejected alternatives.
- Reflection represents Human learning, not an external finding.

That context makes the record safer to transform into an issue, specification, decision record, article, or research task.

## Recording Shows Drift. It Does Not Prevent It.

A Topic record can preserve when the purpose changed, which branch appeared, and why the Human accepted a new direction.

Focused capture can keep unrelated work outside the record. A separate Topic can preserve a useful branch without mixing it into the original task.

But a recorder cannot decide that drift occurred. It cannot know which direction the Human values or maintain the purpose on the Human's behalf.

Direction remains a Human responsibility.

## Check the Result Afterward

At the end, compare intention with reality:

```text
Intended mode:
Actual mode changes:

Expected output:
Actual output:

Resolved questions:
Open questions:

Human decisions:
AI suggestions not yet accepted:
```

This separates decisions from suggestions, findings from hypotheses, and finished work from attractive unfinished branches.

Before your next AI conversation, write:

```text
Topic:
Mode:
Purpose:
Expected output:
Boundary:
Stop condition:
```

Do not enter an AI conversation with only a prompt.

Enter it with a purpose, a mode, and a boundary.

#ArtificialIntelligence #HumanAI #CriticalThinking
