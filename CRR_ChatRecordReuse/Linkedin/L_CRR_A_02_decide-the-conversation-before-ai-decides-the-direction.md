# Decide the Conversation Before AI Decides the Direction

![Human defines the direction and boundaries of an AI conversation](L_CRR_A_02.png)

### A useful AI conversation needs more than a prompt. It needs a purpose, a mode, and a boundary.

Many AI conversations do not fail because the model produces a wrong answer.

They fail because the conversation ends somewhere different from where the Human intended.

You wanted to verify one claim. Several rounds later, you are discussing product strategy.

You wanted a review against requirements. AI began rewriting the document.

You wanted to compare three options. AI proposed five adjacent research directions, and the original decision disappeared.

The new direction may be useful.

The problem is not that every extension is bad. The problem is that the purpose changed without an explicit decision.

---

## AI Is Good at Continuing

Conversational AI can always offer another step:

- a broader framework;
- a related question;
- a new risk;
- an alternative output;
- another improvement;
- or a different problem that sounds more interesting.

That ability is valuable during exploration.

It is less useful when the task is a bounded inquiry, a requirements-based review, or a decision that must converge.

If the Human does not define the intended interaction, plausible continuation can become de facto direction-setting.

This is not about AI having an intention to take control.

It is about the conversation having no visible boundary.

---

## Define a Conversation Contract

Before a substantial AI conversation, define six elements.

### 1. Topic

What continuing subject does this conversation belong to?

Name the work, not the session.

### 2. Mode

What kind of conversation do you need?

Inquiry, Learning, Advisory, Assistance, Discussion, Exploration, Analysis, Creation, Critique, Review, Dialectic, or Reflection?

### 3. Purpose

Why are you having this conversation?

“Discuss this” is vague. “Identify which assumptions make this recommendation unsafe” creates direction.

### 4. Output

What should exist at the end?

A direct answer? A learning note? A comparison? A decision? Review findings? A revised claim? A draft?

### 5. Boundary

What is outside this conversation?

Which topics, files, decisions, audiences, or changes should not be handled now?

### 6. Stop Condition

When should the conversation converge, stop, or create a new topic?

Without a stop condition, each response can generate another plausible task.

---

## Different Modes Need Different Instructions

An inquiry should remain bounded:

```text
Answer this specific question. Identify missing information.
Do not expand into implementation advice.
```

Exploration should intentionally diverge:

```text
Explore possible problem definitions. Do not converge early.
At the end, group the branches and identify separate topics.
```

Analysis should make its basis visible:

```text
Analyze these options using the stated criteria.
Separate facts, assumptions, missing evidence, and conclusions.
```

Review should use explicit standards:

```text
Review this artifact against these requirements.
Report findings and affected sections. Do not make edits.
```

Dialectic should challenge rather than agree:

```text
Give the strongest counterexamples to this claim.
Identify the conditions under which it fails.
```

The prompt is not just a request for content. It assigns a relationship between Human and AI.

The other modes benefit from the same clarity.

Learning should reveal and repair the learner's mental model:

```text
Teach this concept through one concrete example.
Ask me to explain it back, then correct the gaps in my explanation.
```

Advisory should expose trade-offs without silently taking the decision:

```text
Compare these options under my constraints.
State assumptions, risks, and the reason for your recommendation.
Leave the final decision to me.
```

Assistance should support a defined task and label uncertainty:

```text
Help me locate evidence for these three claims.
Separate verified sources from possible leads and unresolved items.
```

Discussion should develop positions rather than force premature agreement:

```text
Discuss this proposal with me.
Track where our positions agree, differ, or change.
```

Creation should identify the artifact and preserve Human direction:

```text
Create a first draft from this brief for this audience.
Do not introduce new product claims. Mark gaps that require my decision.
```

Critique should assess quality without impersonating a rules-based review:

```text
Critique the clarity, structure, and audience fit of this draft.
Explain strengths and weaknesses before suggesting improvements.
```

Reflection should help the Human look back without claiming hidden knowledge:

```text
Help me examine what changed in my reasoning during this project.
Use only the experiences and decisions I provide. Ask about unresolved points.
```

These instructions are not magic formulas. They make the intended relationship visible enough that both the Human and the AI can notice when it changes.

## How a Conversation Drifts

Consider a Human who wants to verify whether one sentence in a product description is supported.

The intended contract is:

```text
Topic: Product claim verification
Mode: Assistance
Purpose: Check the evidentiary basis of one sentence
Output: Supported, unsupported, or qualified, with sources
Boundary: Do not rewrite the page or propose positioning
Stop condition: Evidence is found, disproved, or remains unresolved
```

AI cannot find a decisive source, but suggests a stronger way to describe the product. The Human asks for an example. AI rewrites the paragraph, proposes a new audience, and begins comparing competitors.

Nothing in that sequence is necessarily low quality. Yet the conversation has moved from Assistance to Creation and then toward Advisory. The original claim remains unverified.

Fluency makes the movement feel like progress. The contract reveals that it is a different task.

The Human can now make an explicit choice: return to verification, accept that the claim is unresolved, or open a separate topic for the proposed positioning. What matters is that a useful detour does not masquerade as completion of the original purpose.

---

## Switching Modes Is Allowed

Useful conversations often change mode.

Learning reveals a decision. Analysis uncovers a question that needs exploration. Critique leads to revision. Review leads to reflection.

The problem is not switching.

The problem is switching without noticing.

Suppose the current mode is Analysis and AI proposes three new research directions.

The Human can:

1. remain in Analysis and put the ideas in a backlog;
2. explicitly switch to Exploration;
3. preserve the current work and open a separate Topic.

Each choice can be correct.

Making the choice visible protects the original task from being silently replaced.

A mode change can be written in one line:

```text
Mode change: Analysis → Exploration
Reason: The available evidence exposed three unresolved problem definitions.
The original comparison is paused and will resume after these are separated.
```

That small note prevents later readers—including your future self—from treating exploratory ideas as analytical findings.

---

## Use an Alignment Checkpoint

After several rounds—or whenever AI introduces a major new direction—ask:

```text
Are we still discussing the same Topic?

Are we still using the intended conversation Mode?

Does this direction support the original Purpose?

Is the expected Output still the same?

Should this branch be postponed or opened as a separate Topic?
```

This is a small intervention.

It prevents fluency from being mistaken for alignment.

An alignment checkpoint is especially useful when:

- AI begins producing an artifact you did not request;
- a new question would require different evidence;
- a recommendation appears before the decision criteria are clear;
- the conversation starts optimizing a solution before confirming the problem;
- or “one more improvement” repeatedly delays the expected output.

The checkpoint does not have to interrupt every short exchange. Use it where the cost of drift is higher: consequential decisions, requirements work, published claims, research, or conversations that will be handed to someone else.

## Use the Contract in Team Work

In a team, the contract does more than keep one person focused. It makes delegation and handoff more reliable.

If a colleague receives only a chat transcript, they must infer whether AI was brainstorming, recommending, checking, or producing approved content. That inference can be wrong.

If they receive the Topic, Mode, Purpose, expected Output, Boundary, and Stop Condition, they can interpret the record more carefully:

- an Exploration record contains possibilities, not commitments;
- an Advisory record contains a recommendation, not necessarily a decision;
- a Review finding should point to the requirement it used;
- a Creation record may contain rejected alternatives as well as the chosen draft;
- a Reflection record represents Human learning, not an external finding.

This makes the conversation easier to continue and safer to transform into a decision record, issue, specification, article, or research task.

---

## Recording Helps You See Drift. It Does Not Prevent It.

A topic record can preserve when the purpose changed, which branches appeared, and why a new direction was accepted.

A focused start-and-stop capture can keep unrelated work out of the record. A separate topic can preserve a valuable branch without mixing it into the current one.

But a recorder cannot decide that drift has occurred.

It cannot know which direction the Human values. It cannot maintain the purpose on the Human's behalf.

Direction remains a Human responsibility.

## Inspect the Conversation After It Ends

The conversation contract is useful after the session as well as before it.

Compare the intended and actual interaction:

```text
Intended mode:
Actual mode or mode changes:

Expected output:
Actual output:

Questions resolved:
Questions still open:

New branches worth preserving:
Branches that should remain outside this topic:

Human decisions made:
AI suggestions not yet accepted:
```

This short inspection turns a fluent transcript into material that can be reused responsibly. It separates decisions from suggestions, findings from hypotheses, and finished work from attractive unfinished branches.

If the conversation drifted, the answer is not always to delete the detour. A useful branch can become its own topic. The original record can retain a short link explaining where it went and why.

---

## Before Your Next AI Conversation

Write this first:

```text
Topic:
Mode:
Purpose:
Expected output:
Boundary:
Stop condition:
```

Then start the conversation.

The question is not only:

> What should I ask AI?

It is also:

> **What kind of conversation do I need, and what must still be true when it ends?**

#ArtificialIntelligence #PromptEngineering #HumanAI #Productivity #CriticalThinking
