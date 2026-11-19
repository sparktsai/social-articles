# Before You Talk to AI, Choose the Conversation

![Human sets the purpose mode and boundary before talking to AI](illustrations/M_CRR_A_10.png)

> Do not enter an AI conversation with only a prompt. Enter it with a purpose, a mode, and a boundary.

Many AI conversations do not fail because the model produces a bad answer.

They fail more quietly.

The conversation begins with one purpose, moves through several useful-looking responses, and ends somewhere else.

You wanted to verify one factual claim. A few rounds later, you are discussing product strategy.

You wanted a review against stated requirements. AI started rewriting the document.

You wanted to compare three options. AI proposed five adjacent research directions, and the original decision disappeared.

The new direction may be interesting. It may even be valuable.

The problem is that the purpose changed without an explicit decision.

---

## AI Is Designed to Continue

Conversational AI is good at offering more.

It can suggest related questions, additional steps, alternative formats, new risks, broader frameworks, and possible improvements. That behavior often makes the interaction feel productive.

But “more” is not always aligned with the task.

If the Human has not defined the intended conversation, AI's ability to extend can become de facto direction-setting.

This does not mean AI has intentions or has deliberately taken control. It means the interaction lacks a visible boundary, so each plausible continuation is allowed to redefine the work.

The Human remains responsible for deciding:

- what topic is being addressed;
- what kind of interaction is needed;
- what output should exist at the end;
- and which attractive branches should wait.

---

## A Prompt Describes a Request. A Conversation Contract Describes the Work.

Before starting, define six things.

### 1. Topic

What continuing subject does this conversation belong to?

Use a name that describes the work, not the session.

### 2. Mode

What kind of Human–AI relationship do you need?

Inquiry? Learning? Advice? Assistance? Discussion? Exploration? Analysis? Creation? Critique? Review? Dialectic? Reflection?

### 3. Purpose

Why are you having this conversation?

“Discuss this” is weak. “Identify which assumptions make this recommendation unsafe” is stronger.

### 4. Output

What should exist when the conversation ends?

A direct answer? A learning note? A comparison? A decision? A list of review findings? A revised claim? A draft?

### 5. Boundary

What should not be handled in this conversation?

Which files, topics, decisions, audiences, or adjacent problems are out of scope?

### 6. Stop Condition

When should the conversation end, converge, or create a new topic?

Without a stop condition, every answer can generate another plausible task.

---

## The Twelve Modes Need Different Prompts

### Inquiry

Ask for a bounded answer. State whether adjacent suggestions are welcome.

```text
Answer this specific question. If the answer depends on missing information,
identify it. Do not expand into implementation advice.
```

### Learning

Ask for a sequence that changes understanding, not only a result.

```text
Teach this from first principles, then give me one example and ask a question
that checks whether I understood it.
```

### Advisory

Define the decision, constraints, and ownership.

```text
Compare these options under the stated conditions. Show trade-offs and
uncertainty. I will make the final decision.
```

### Assistance

Name the primary task and limit AI to a supporting role.

```text
I am writing a sourced article. Identify possible primary sources for this
claim and mark anything you cannot verify. Do not draft the article.
```

### Discussion

Allow exchange while keeping the topic stable.

```text
Discuss this position with me. Surface different viewpoints, but keep the
conversation within this question.
```

### Exploration

Make divergence intentional.

```text
Explore possible problem definitions. Do not converge too early. At the end,
group the branches and identify which deserve separate topics.
```

### Analysis

Fix the question, assumptions, and criteria before deriving a conclusion.

```text
Analyze these options using the listed criteria. Separate known facts,
assumptions, missing evidence, and conclusions.
```

### Creation

Define the artifact, audience, purpose, and Human control.

```text
Help draft a Medium article for experienced AI practitioners. Preserve my
core claim and flag any new claim you introduce.
```

### Critique

Specify the lens.

```text
Critique this explanation for clarity and usefulness to a developer who is
new to the concept. Do not rewrite it yet.
```

### Review

Provide standards, scope, and acceptance conditions.

```text
Review this document against the listed requirements. Report findings with
the affected section and requirement. Do not make edits.
```

### Dialectic

Ask for opposition, not agreement.

```text
Challenge this claim. Give the strongest counterexamples and identify the
conditions under which it would fail.
```

### Reflection

Keep the Human's change at the center.

```text
Compare my initial and current positions. Ask what changed my judgment and
what remains unresolved. Do not decide the lesson for me.
```

---

## Mode Switching Is Not the Problem

A conversation does not need to remain in one mode.

Learning can reveal a decision. Analysis can expose a question that requires exploration. Critique can lead to creation. Review can lead to reflection.

The problem is an unacknowledged switch.

Suppose the mode is Analysis. AI identifies three new research directions.

The Human has three valid choices:

```text
Stay in Analysis
  Add the new directions to a backlog and finish the current judgment.

Switch to Exploration
  Explicitly change the purpose and accept divergence.

Create a New Topic
  Preserve the current analysis and continue the new direction separately.
```

Making the choice visible protects both threads of work.

---

## Use an Alignment Checkpoint

Every few rounds—or whenever AI introduces a major new direction—ask:

```text
Are we still discussing the same topic?

Are we still using the intended conversation mode?

Does the current direction support the original purpose?

Is the expected output still the same?

Should this branch be postponed or recorded as a separate topic?
```

This is not bureaucratic overhead.

It is a lightweight way to stop fluency from being mistaken for alignment.

---

## How Recording Helps—and What It Cannot Do

Starting a topic record can make the boundary more visible. A focused start-and-stop capture can preserve only the relevant discussion. A later review can show when the mode changed and which branch became a new purpose.

But a recorder cannot maintain alignment by itself.

It cannot decide that the conversation has drifted. It cannot know which new direction the Human values. It cannot automatically separate every branch into the right topic.

Recording supports reflection and reuse.

Direction remains a Human decision.

---

## Start with a Conversation Card

Before your next substantial AI conversation, write this:

```text
Topic:
Mode:
Purpose:
Expected output:
Boundary:
Stop condition:
```

It takes less than a minute.

It changes the relationship from “keep responding until something useful appears” to “work toward an explicit outcome, and make any change of direction visible.”

The first question before talking to AI should not only be:

> What should I prompt?

It should also be:

> **What kind of conversation do I need, and what must still be true when it ends?**

Chat Record Reuse · 10 / 10

#ArtificialIntelligence #PromptEngineering #Productivity #CriticalThinking #AIAssistants
