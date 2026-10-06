# X Post Pattern Library

適用於 AI、Software Engineering、QA、Governance、Knowledge、Agent、SDLC 等技術主題的 X Post 句型庫。

---

## 1. A 不等於 B

```text
A ≠ B.

很多人把 A 當成 B。
但真正差異在於 ______。

如果沒有 ______，
你其實仍然只有 A。
```

適用：
- Document ≠ Knowledge
- RAG ≠ Knowledge
- Code Review ≠ RTM
- AI Agent ≠ Agentic Workflow

---

## 2. 問題 → 可能解法 → 選擇

```text
當 ______ 發生時，你會怎麼處理？

A？
B？
C？

我目前用的是 ______。

你會選哪一個？
```

重點：
讓讀者容易直接回 A / B / C，而不是需要寫長篇答案。

---

## 3. 問題 → 本質

```text
表面上的問題是 ______。

但真正的問題可能不是 ______。

而是 ______。
```

例：

```text
The problem isn't that AI generates bad code.

The problem is that we often cannot prove
why the generated code is correct.
```

---

## 4. 大家都在做 A → 但沒人在問 B

```text
Everyone is talking about A.

But I rarely see people asking B.

And B may actually determine whether A works.
```

例：

```text
Everyone is talking about AI code generation.

But who defines the acceptance boundary?
```

---

## 5. 工具很容易 → 真正困難的是另一層

```text
Doing A is easy.

Doing B is harder.

But B is where the real engineering problem begins.
```

例：

```text
Generating tests with AI is easy.

Defining what must be tested is harder.
```

---

## 6. 如果 AI 做 A，那誰負責 B？

```text
If AI does A,
who does B?

Who defines C?
Who verifies D?
Who owns the result?
```

例：

```text
If AI writes the code,
who writes the test spec?
Who writes the tests?
Who decides what "passed" means?
```

---

## 7. 以前是 A → 現在是 B

```text
We used to ______.

Now we ______.

The interesting question is:
what changed in between?
```

適合：
- 軟體測試史
- Code Review 演化
- QA 演化
- SDLC 演化
- AI-assisted development

---

## 8. 能力不是問題 → 邊界才是問題

```text
Can AI do A?

Probably.

The more important question is:
where should AI stop?
```

替代版本：

```text
The question is no longer whether AI can do it.

The question is who defines the boundary.
```

---

## 9. 三件事看起來一樣 → 其實是三個不同問題

```text
A, B, and C are often discussed as if they were the same thing.

They aren't.

A asks ______.
B asks ______.
C asks ______.
```

適合：
- Auth / Policy / Governance
- Runtime Decision / Development Decision
- Requirement / Test / Acceptance
- Retrieval / Knowledge / Evidence

---

## 10. 我原本以為 A → 做完才發現 B

```text
I started with A.

After building/testing it,
I realized the real problem was B.

That changed how I think about ______.
```

適合：
- 實作心得
- 實驗結果
- Side Project
- OSS
- Research observation

---

## 11. 最容易自動化的，不一定是最重要的

```text
The easiest part to automate is A.

The most important part may be B.

And they are not the same problem.
```

例：

```text
Generating test cases is easy.

Defining the test boundary is not.
```

---

## 12. 缺少的一層

```text
We already have A.
We already have B.
We already have C.

What seems to be missing is D.
```

適合：
- 提出新 framework
- 提出新 primitive
- 指出現有工具鏈缺口
- 引出 evidence / boundary / scope / traceability

---

## 13. 同樣輸入 → 為什麼結果不同？

```text
Same requirement.
Same model.
Same repository.

Different result.

What actually changed?
```

可引向：
- Context
- Scope
- Boundary
- Evidence
- Prompt
- State
- Tool access
- Runtime condition

---

## 14. 你測的是 A，還是其實只測了 B？

```text
Are you testing A?

Or are you only testing B?
```

例：

```text
Are you testing the AI agent?

Or only its final answer?
```

---

## 15. 可以做到 ≠ 可以證明

```text
AI can do A.

But can you prove:
- why it did it?
- whether it was allowed?
- what changed?
- whether it can be reproduced?
```

適合：
- Governance
- Evidence
- Auditability
- Runtime decision
- Agent behavior
- AI-generated code

---

## 16. 最通用的 X Post 結構

```text
Hook
→ Tension
→ Reframe
→ Question
```

例：

```text
AI can generate thousands of test cases.

That's not the hard part.

The hard part is deciding
what must be tested,
what must never change,
and what counts as passing.

Who defines that in your AI development workflow?
```

---

## 最適合長期反覆使用的四種母型

```text
1. A ≠ B

2. Everyone talks about A, but ignores B

3. If AI does A, who owns B?

4. Surface problem A / Real problem B
```

這四種特別適合 AI Engineering、Software Testing、Governance、Knowledge、Agent、Evidence、Boundary 類主題，因為可以把抽象觀點快速轉成低閱讀成本、容易回覆的 X Post。
