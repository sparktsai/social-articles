---
name: write-x-article
description: Create, rewrite, or review long-form X Articles for technical subjects such as AI engineering, software engineering, QA, governance, knowledge systems, agents, evidence, and SDLC. Use when producing an X Article, adapting source material into an X Article, planning an X Article series, or checking an Article for platform fit, narrative clarity, evidence, mobile readability, and distribution readiness.
---

# Write X Articles

Create a publish-ready X Article that makes one defensible claim for one identifiable audience.

## Required reference

Read [articles-guide.md](articles-guide.md) completely before drafting or reviewing an Article. Treat it as the authoritative platform and editorial guide. Use [post.md](post.md) only when creating teaser Posts, follow-up Posts, or threads for distribution.

If current X product behavior, eligibility, formatting, or recommendation guidance matters, verify it against official X sources before writing. Distinguish official statements from inferences. Never promise reach, virality, or algorithmic promotion.

## Gather the brief

Derive these fields from the user's request and supplied materials:

```text
Topic:
Target audience:
Desired reader change:
Core claim:
Evidence or source material:
Language:
Desired length:
Call to action:
Output location:
```

Infer missing fields when the context supports a safe choice. Ask only when a missing answer would materially change the article. Default to the language of the requested output or source material.

Do not invent facts, results, quotations, customer stories, statistics, or personal experience. Mark unsupported placeholders explicitly or research them when the user authorizes or requires current facts.

## Build the argument

Before drafting, create an internal one-sentence statement for each item:

1. **Audience** — the specific role or group this Article serves.
2. **Change** — what the reader should think, decide, or do differently.
3. **Claim** — the single conclusion the Article will establish.
4. **Tension** — why the common framing or current practice is insufficient.
5. **Evidence** — what makes the claim credible.
6. **Boundary** — where the claim does not apply or needs qualification.

Split the work into multiple Articles when the claim requires two independent conclusions joined by “and.”

Choose the smallest structure that proves the claim. Prefer this sequence for technical viewpoint Articles:

```text
Recognizable situation
→ Tension or failure mode
→ Reframe and core claim
→ Model or explanation
→ Evidence and example
→ Practical application
→ Boundary or counterexample
→ Takeaway and focused question
```

Do not introduce a framework before the reader understands the problem it resolves.

## Draft the Article

### Title

Write a specific, credible title that identifies a problem, contrast, consequence, or useful answer. Create 3–5 candidate titles internally and select the one that best matches the actual evidence.

Avoid generic topic labels, unsupported numbers, exaggerated certainty, and curiosity gaps that hide the subject.

### Opening

Use the first 3–5 short paragraphs to establish:

1. A situation the target reader recognizes.
2. A contradiction, cost, or missing layer.
3. The Article's core claim.
4. What the reader will understand or be able to do.

Do not begin with broad historical background, dictionary definitions, or generic statements about rapid technological change.

### Body

Make each section advance one question. Use the pattern:

```text
Claim → Evidence → Meaning
```

Use concrete decisions, roles, artifacts, boundaries, and observable behaviors. When discussing abstract concepts such as governance, knowledge, agents, or quality, translate them into questions such as:

- Who made which decision, and when?
- Which rule, context, or version was used?
- What evidence was retained?
- What condition defines acceptance or failure?
- Who verifies and owns the result?

Support material claims with supplied evidence, first-hand observations clearly identified as such, or cited sources. Include a limitation, boundary, or meaningful counterexample when appropriate.

### Formatting

Optimize for mobile skimming:

- Keep most paragraphs to 2–4 lines.
- Use one idea per paragraph.
- Add a descriptive subheading after roughly 3–5 paragraphs when the argument changes stage.
- Prefer lists for genuinely parallel items, not for every thought.
- Bold only conclusions worth finding during a scan.
- Recommend a visual only when it supplies evidence or reduces explanation cost.

### Ending

Close by:

1. Restating the core claim without copying the opening.
2. Giving the reader a concrete decision, diagnostic, or next action.
3. Asking one specific, low-friction question that extends the subject.

For a series, optionally preview the next Article without weakening the current ending.

## Prepare distribution assets

When the user asks for a complete publishing package, append these after the Article under clearly separate headings:

1. **Header image brief** — concept, focal element, composition, and any on-image text.
2. **Pre-publication teaser** — one short Post that tests or introduces the tension without summarizing the whole Article.
3. **Launch Post** — a standalone insight plus a natural reason to read the Article.
4. **Follow-up Posts** — 2–4 distinct angles drawn from a case, model, counterexample, diagram, or practical diagnostic.
5. **Reply prompt** — one focused question for substantive discussion.

Use [post.md](post.md) for Post patterns. Every promotional Post must provide independent value; do not produce repeated link drops or engagement bait.

Do not add distribution assets when the user requests only the Article.

## Review gates

Revise until all applicable checks pass.

### Argument

- The target reader is identifiable.
- The Article establishes one primary claim.
- The tension appears before the framework or solution.
- Each major section contains a claim, support, and implication.
- Material assertions are evidenced or clearly qualified.
- Limitations or applicability boundaries are addressed.
- The conclusion follows from the body.

### Platform fit

- The title is specific and fulfilled by the Article.
- The opening establishes value within 3–5 short paragraphs.
- Paragraphs and sections are readable on mobile.
- Formatting improves comprehension rather than decorating the page.
- The final question is specific enough to answer meaningfully.
- No wording promises recommendation, reach, or virality.

### Voice

- The tone is analytical, direct, and conversational rather than academic or promotional.
- Technical precision is preserved without unnecessary jargon.
- Generic AI prose, filler transitions, repeated conclusions, and inflated claims are removed.
- The Article has a recognizable point of view but does not overstate certainty.

### Integrity

- No fact, quote, statistic, result, or experience is fabricated.
- Current platform claims are verified when they affect the result.
- Official guidance and strategic inference are labeled separately.
- Source links point directly to the supporting material.

## Deliver the result

Unless the user requests another format, return:

```markdown
# [Selected title]

[Publish-ready Article]

## Sources

- [Direct source links, only when sources were used]
```

Do not expose internal planning notes unless the user requests an outline or editorial rationale. If writing to the repository, follow its existing platform, series, and filename conventions and preserve unrelated working-tree changes.
