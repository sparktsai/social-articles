# Did the AI Actually Understand My Intent?

I am running an experiment: can I develop software through No-Code without giving up software quality?

To make the constraint real, I chose a programming language I have never learned, and I do not review the generated code.

I want to discover what problems emerge when a human must judge software quality without reading the code—and what evidence, controls, and decisions are needed in response.

The first problem appeared even though I let Claude Code use `/review` to ask me questions.

The interaction looked careful. AI asked which behavior should remain compatible, how a case should be handled, and which implementation choice I preferred.

But those questions were based on Intent assumptions AI had already made. It was asking how to implement its interpretation—not trying to discover whether that interpretation matched mine.

Only after the implementation was complete did I find the gap: something I considered common knowledge was not knowledge I could assume AI already had.

The problem was not that AI asked no questions. It was that implementation clarification and Intent confirmation had been treated as the same thing.

```text
Implementation clarification: How should this be built?
Intent confirmation: Are we building the right thing?
```

AI does not implement Human Intent directly. It first constructs an interpretation. The Specification, Code, and Tests are then derived from it.

Everything below that interpretation can be internally consistent—and still solve the wrong problem.

```text
Human Intent
→ AI-understood Intent
→ Specification
→ Code and Tests
```

A passing Test can show that the Code satisfies the Specification. It cannot show that the Specification represents what the Human meant.

Before implementation, AI should expose a reviewable interpretation:

- the problem it believes the Human wants to solve;
- the expected observable outcome;
- assumptions it added;
- included and excluded boundaries;
- ambiguous points; and
- decisions that still require Human confirmation.

The Human does not need to review Code at this stage. The Human needs to confirm meaning.

That confirmed interpretation should then remain traceable through the Specification, Acceptance Criteria, implementation, and Test Evidence.

No process can reveal every unstated expectation. But hidden assumptions should not masquerade as confirmed requirements.

In No-Code development, software quality begins before Code generation—with a reviewable and correctable account of what the AI believes the Human meant.

**What would you need to see before accepting an AI-generated Specification as an accurate representation of your Intent?**

No-Code Quality · 01 / 06

#NoCodeQuality #RequirementsEngineering #HumanInTheLoop
