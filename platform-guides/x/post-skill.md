---
name: write-x-post
description: Create, rewrite, adapt, or review short-form X content for technical subjects such as AI engineering, software engineering, QA, governance, knowledge systems, agents, evidence, and SDLC. Use when producing standalone Posts, Replies, Mentions, Quote Posts, Polls, Longer Posts, or threads; extracting Posts from an Article; creating teaser, launch, or follow-up Posts; or checking content for clarity, platform fit, credibility, conversational value, policy safety, and publish readiness.
---

# Write X Posts

Create a publish-ready X Post that communicates one recognizable idea with low reading cost and a clear reason to respond, remember, or continue reading.

## Required reference

Read [post-guides.md](post-guides.md) completely before drafting or reviewing Posts. Treat it as the authoritative platform, editorial, distribution, and policy guide. Use its pattern library as a set of options rather than mandatory templates. Select a pattern only when it naturally fits the source idea.

When adapting a long-form X Article, read the source Article. Read [articles-guide.md](articles-guide.md) only if the task also requires changing the Article or planning the relationship between the Article and its Post series.

If current X limits, features, or recommendation guidance affect the requested result, verify them against official X sources. X documentation for Longer Posts can change or disagree across pages, so check the current Help Center or composer whenever an exact limit matters. Separate official statements from strategic inference. Never promise reach, virality, or algorithmic promotion.

## Gather the brief

Derive these fields from the request and supplied material:

```text
Topic:
Target reader:
Core point:
Desired response:
Evidence or source material:
Language:
Format: standalone | reply | mention | quote | thread | poll | article teaser | article launch | follow-up
Length or post count:
Link or call to action:
Output location:
```

Infer missing fields when context makes the choice safe. Ask only when a missing answer would materially change the result. Default to the requested or source language.

Do not invent facts, statistics, quotations, product behavior, customer stories, experiments, or personal experience. Research current claims when required, or mark unsupported details explicitly.

## Distill the idea

Before writing, state internally:

1. **Observation** — what concrete situation does the reader recognize?
2. **Tension** — what assumption, gap, contrast, or ownership question makes it interesting?
3. **Point** — what single conclusion should remain after reading?
4. **Support** — what example, mechanism, or evidence makes the point credible?
5. **Response** — what useful reaction should the Post invite?

If the Post needs two independent conclusions, split it into separate Posts or a thread.

## Route to a pattern

Choose a pattern by the rhetorical job the Post must perform. Use the numbered definitions and full examples in [post-guides.md](post-guides.md).

| Rhetorical job | Preferred pattern |
| --- | --- |
| Separate two concepts readers commonly conflate | 1. A is not B |
| Offer meaningful alternatives with a low-friction response | 2. Problem → possible solutions → choice |
| Replace a visible symptom with the underlying cause | 3. Surface problem → real problem |
| Challenge an incomplete mainstream discussion | 4. Everyone discusses A but ignores B |
| Move attention from an easy action to the hard engineering layer | 5. A is easy → B is harder |
| Expose ownership, verification, or accountability gaps | 6. If AI does A, who owns B? |
| Compare historical or process evolution | 7. We used to A → now we B |
| Shift debate from capability to limits or control | 8. Capability is not the issue → boundary is |
| Separate several ideas incorrectly treated as one | 9. A, B, and C are different problems |
| Share a first-hand build, test, or research discovery | 10. I started with A → discovered B |
| Contrast what is easy to automate with what matters | 11. Easiest to automate ≠ most important |
| Name a missing primitive, framework, or toolchain layer | 12. The missing layer |
| Diagnose inconsistent outcomes from apparently equal inputs | 13. Same input → different result |
| Challenge what a test or evaluation actually measures | 14. Are you testing A, or only B? |
| Contrast execution capability with evidence and auditability | 15. Can do ≠ can prove |
| Use a compact default when no more specific pattern dominates | 16. Hook → tension → reframe → question |

Apply this selection process:

1. Identify the Post's primary rhetorical job.
2. Select one preferred pattern; use a second only when it adds a necessary logical step.
3. Reject a pattern if it requires a claim, experience, comparison, or set of options not supported by the source material.
4. Rewrite the pattern in the author's natural voice; never expose blanks or template wording.
5. Compare the draft against Pattern 16 and keep the version with the clearest movement and lowest reading cost.

If two patterns fit equally well, choose the one that makes the core point understandable with less context. Do not cycle through patterns merely to create superficial variants.

## Choose the format

### Standalone Post

Use when one claim can be understood without prior context. Apply the selected pattern as an argument shape, not a fill-in-the-blank template. Rewrite or combine patterns when the idea requires a more natural voice.

Default to a standard Post when the idea can fit clearly within the current ordinary Post limit. Use a Longer Post only when additional context materially improves comprehension; verify current account eligibility and product limits when they affect delivery.

### Reply

Use to answer, clarify, challenge, or extend a specific Post. Make the relationship to the parent Post explicit. Never use unrelated or templated Replies to divert traffic.

### Mention

Use only when notifying or addressing a specific account is relevant. A Post beginning with `@username` can have different Home timeline visibility from a general Post. If the goal is to share someone else's content with all followers, prefer a Quote Post with substantive commentary.

### Quote Post

Add an interpretation, implication, counterexample, or useful context that can stand on its own. Do not merely repeat the quoted Post or write an empty endorsement.

### Poll

Use when the choices themselves clarify meaningful alternatives and lowering reply effort is valuable. Do not reduce a question that requires reasoning to arbitrary options.

### Thread

Use only when the idea genuinely requires ordered reasoning, multiple examples, a process, or a sequence that cannot fit clearly in one Post.

Structure a thread as:

```text
Post 1: Core tension and reason to continue
Post 2: Context or common framing
Post 3+: One claim, example, or step per Post
Penultimate Post: Reframe or synthesis
Final Post: Takeaway and focused question or action
```

Make every Post understandable enough that a reader entering mid-thread can follow it. Do not fragment sentences or use many Posts to inflate a simple idea.

### Article teaser

Introduce the unresolved question or tension before publication. Do not summarize the entire Article or pretend it is already published.

### Article launch Post

Give the reader one complete insight, then explain what additional model, evidence, or application the Article provides. Avoid a bare link announcement.

### Article follow-up Post

Extract one distinct asset from the Article:

- a counterintuitive claim;
- a concrete example;
- a diagram or framework;
- a failure mode;
- a practical diagnostic;
- a limitation or counterexample.

Each follow-up must deliver independent value and use a different angle rather than repeating the launch copy.

## Draft the Post

### Opening

Start with the idea, tension, or concrete situation. Make the first lines specific enough that the intended reader can recognize relevance without needing background.

Avoid:

- generic scene-setting about rapid change;
- empty declarations such as “Here are my thoughts”;
- unearned certainty or outrage;
- a question so broad that any answer is equally valid;
- clickbait that hides the actual subject.

### Body

Develop one logical movement:

```text
Hook → Tension → Reframe → Question or takeaway
```

Use short paragraphs and deliberate line breaks. Prefer concrete roles, decisions, boundaries, inputs, outputs, and evidence over abstract nouns.

For technical themes, move beyond “Can AI do this?” and consider:

- Who defines the boundary?
- Who verifies the result?
- What evidence supports the decision?
- What changed between two different outcomes?
- What does “passed” mean here?
- Who owns the consequence?

Do not over-explain. Preserve enough context to prevent ambiguity, then stop after the claim lands.

### Ending

Choose one ending that fits the purpose:

- a concise reframe;
- a specific diagnostic;
- a low-friction question;
- a practical next action;
- a natural link to a full Article.

Ask a question only when the answer would contribute to the topic. Avoid engagement bait, forced A/B choices without meaningful tradeoffs, and generic “Thoughts?” endings.

## Preserve voice

Write in an analytical, direct, conversational voice. Favor clear contrasts, ownership questions, engineering boundaries, and observable consequences.

Use technical terms when they improve precision. Remove corporate filler, generic motivational language, excessive hashtags, repeated conclusions, and polished-but-empty AI prose.

Allow uncertainty where evidence is limited. A strong point of view can still state its conditions and boundaries.

## Create variants only when useful

When the user asks for options, produce 2–4 meaningfully different approaches, such as:

- contrast-led;
- question-led;
- evidence-led;
- story or build-observation-led.

Do not return superficial synonyms as variants. Label the strategic difference briefly, then recommend the strongest option when enough context exists.

## Review gates

Revise until all applicable checks pass.

### Idea

- The target reader and topic are recognizable immediately.
- The Post communicates one primary point.
- The tension supports the conclusion instead of manufacturing drama.
- The conclusion follows from the example or reasoning.
- Technical abstractions are connected to observable behavior.

### Readability

- The opening reaches the subject without generic preamble.
- Every line contributes information, tension, rhythm, or clarity.
- Paragraphs and line breaks are easy to scan on mobile.
- The Post is no longer than the idea requires.
- A thread is used only when sequence or depth justifies it.
- A network-external reader can understand the Post without missing prior context.
- Exact length and product constraints are verified when a Longer Post is requested.

### Conversation

- Any question is specific and easy to answer meaningfully.
- The Post offers value before requesting a response or click.
- Article promotion is not a bare link drop.
- Follow-up Posts use distinct angles and do not repeat identical copy.
- Replies and Quotes contribute information rather than redirecting attention without relevance.

### Integrity

- No fact, quote, statistic, result, or experience is fabricated.
- Claims are supported, qualified, or framed explicitly as opinion.
- Current platform claims are verified when relevant.
- The Post does not promise reach, virality, or recommendation.
- The Post avoids spammy repetition and engagement manipulation.
- Hashtags and mentions are relevant and limited to a genuine content purpose.
- The Post is not identical or near-identical to recent planned outputs.
- Media carries information value, and accessibility text or captions are provided when requested as part of the publishing package.

## Deliver the result

Unless another format is requested, return only the publish-ready copy in a fenced `text` block so it can be copied without surrounding commentary.

For a thread, label Posts outside the copy or separate them with a clear divider. Do not place numbering inside the published text unless numbering improves the reading experience.

When sources were used, list direct links after the copy under `Sources`; do not place citation clutter inside a short Post unless the citation itself is part of the content.

If writing to this repository, follow its existing platform, series, and filename conventions. Preserve unrelated working-tree changes.
