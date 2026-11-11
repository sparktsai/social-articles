## Relay 1 — Three assertions

Three assertions about AI-assisted testing:

1. Software testing has increasingly moved toward business requirements and visible acceptance behavior. That alignment is valuable—but it can leave internal invariants, exception paths, concurrency, resource handling, and other less-visible engineering concerns under-tested.

2. In practice, SDD often functions as an AI contract between Vibe Coding and a complete formal specification. Its center of gravity is still frequently the requirement and visible behavior—not every engineering property the implementation must preserve.

3. Tests that AI adds by itself are inferred tests. They are derived from prompts, specifications, code, nearby tests, and familiar patterns. They are useful, but they are not automatically proof of engineering correctness.

When code and tests are inferred from the same context, a green result may demonstrate consistency between generated artifacts—not correctness against engineering reality that was never included in that context.

## Relay 2 — How to ensure AI software quality

AI should not simultaneously be the requirements author, implementer, test designer, and final judge.

AI-generated software needs independent evidence:

• humans own critical business rules, risks, and unacceptable outcomes;
• acceptance tests and release gates cannot be silently rewritten by the implementation agent;
• mocks are complemented by contract tests and tests against real dependencies;
• boundary, negative, state-transition, concurrency, and failure-path tests are designed systematically;
• performance, security, reliability, recovery, and observability have measurable requirements;
• changes to assertions, snapshots, expected results, and test exclusions are audited;
• monitoring, canary releases, rollback, and incident learning remain part of QA.

“All tests passed” tells us that selected tests accepted selected behavior.

It does not tell us whether the right risks were selected.

Has QA disappeared in the AI software era—or have we simply not yet developed QA methods and tools that match how AI generates software?
