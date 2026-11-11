# How Do You Ensure the Quality of AI-Generated Code?

“All tests passed” sounds like evidence that software is ready.

But what if the implementation, the tests, and the test report were all produced by the same AI from the same incomplete specification?

Do you review AI-generated code? Do you ask AI to produce a test report and then audit that report? Do you independently execute its test code to verify the result?

These questions are not about distrusting AI. They are about determining what the available evidence actually proves.

## Where the question began

My question began with Vibe Coding applications that passed their tests but were still not truly usable. The tests often covered the user interface and a few end-to-end happy paths. They did not adequately cover exceptions, data boundaries, dirty production data, operational failures, or real execution environments.

I then wondered whether a more structured workflow would solve the problem. If we include non-functional requirements and add explicit test specifications to Specification-Driven Development, can we ensure the quality of AI-generated code?

While examining edge cases, I encountered a deeper limitation. AI can generate familiar boundary cases, invalid inputs, and exception tests. But without the relevant business rules, data constraints, risk models, production history, and past incidents, it can test only what it can infer from the context provided.

The problem is therefore not simply whether we have enough tests. It is:

**Who defines the correct result, and how do we know that the test itself is correct?**

## How software quality evidence evolved

Software testing has never been one activity.

Traditional or regulated projects often expressed quality through formal artifacts. A Qualification Test Report documented whether a system satisfied its qualification requirements. An Acceptance Test Report recorded whether the delivered system met the conditions for acceptance.

Agile teams increasingly used acceptance criteria to define when a feature should be considered complete. But acceptance criteria did not replace test reports:

- acceptance criteria define the conditions for accepting a requirement;
- test reports record what was tested, what passed, what failed, and what risks remain.

The format changed, but the need for evidence did not disappear.

Several development methods also connected tests more closely to design and requirements.

Test-Driven Development uses a failing test to guide implementation and refactoring. It is commonly associated with unit or component feedback.

Acceptance Test-Driven Development brings business representatives, developers, and testers together to define acceptance examples before implementation.

Behavior-Driven Development describes behavior through shared domain language. Given–When–Then makes context, action, and expected outcome visible to both business and technical participants.

TDD, ATDD, and BDD are not a linear sequence in which one replaced another. They can coexist because they answer different questions.

## Three assertions about AI-assisted testing

### 1. Attention has moved toward visible business behavior

Modern delivery increasingly emphasizes user journeys, acceptance criteria, examples, and externally visible outcomes. This aligns development with business intent.

But it can also move attention away from less-visible engineering concerns: internal invariants, exception paths, numerical boundaries, resource handling, concurrency, data corruption, and failure recovery.

A feature can satisfy every visible acceptance example while remaining weak at the engineering level. Business-facing behavior and implementation-level correctness are complementary evidence. Neither replaces the other.

### 2. SDD often acts as an AI contract

Many practical forms of Specification-Driven Development sit somewhere between Vibe Coding and a complete formal specification.

The specification acts as an AI contract. It preserves intent, constraints, tasks, and acceptance conditions so the agent has something more stable than a conversational prompt.

This reduces ambiguity and improves traceability. Yet its center of gravity often remains at the requirement and observable-behavior level. Unless engineering constraints are explicit, the workflow may still omit resource limits, concurrency behavior, migration safety, rollback conditions, observability, and failure semantics.

An AI contract is only as complete as the engineering knowledge encoded within it.

### 3. AI-generated tests are inferred tests

When AI adds tests by itself, it infers them from the prompt, specification, existing code, nearby tests, and familiar testing patterns.

These inferred tests can be valuable. They may reveal real defects. But they are not automatically engineering-correctness tests.

Engineering correctness needs an independent basis for deciding what must always hold: architecture rules, domain invariants, threat models, interface contracts, numerical properties, operational limits, historical failures, or expectations validated by accountable stakeholders.

If AI infers both implementation and tests from the same context, a passing result primarily demonstrates consistency between generated artifacts. It does not prove correctness against engineering reality absent from that context.

## Test levels and test types answer different questions

Test levels describe where verification occurs:

- unit or component tests verify an individual function, class, or module;
- component integration tests verify interactions inside a system;
- system tests evaluate the complete system;
- system integration tests verify external interfaces and services;
- acceptance tests determine whether the system satisfies business needs and is ready for use.

End-to-end testing follows a complete user or business flow, potentially across several systems. It proves that a selected journey works under selected conditions. It does not prove that every relevant quality risk has been addressed.

Test types describe what quality is being evaluated. Functional testing asks whether required behavior is correct. Non-functional testing examines qualities such as performance, security, reliability, usability, compatibility, and maintainability.

Structural tests examine internal paths and coverage. Change-related tests confirm fixes and detect regressions.

A system can pass functional tests and still be unusable because it is slow, insecure, unreliable, inaccessible, or operationally unsafe.

## Quality is more than functional correctness

Software quality includes at least three perspectives:

1. Functional correctness: does the system do what the specification says?
2. Non-functional quality: how securely, reliably, efficiently, and maintainably does it behave?
3. Fitness for purpose: does it solve the actual user and business problem?

Non-functional requirements must be measurable. “The system must be fast” is not a useful release gate. Better conditions include:

- 95% of API requests complete within 300 milliseconds;
- recovery after failure takes no more than 15 minutes;
- one tenant cannot read another tenant's data;
- errors remain below 0.1% under a defined concurrent load.

Writing these conditions into a specification is not the same as verifying them. Verification still needs representative data, environments, tools, and release thresholds.

## The test oracle problem

Every test needs an oracle: a way to decide whether an observed result is correct.

A test can show that implementation behavior matches the expectation encoded in the test. If that expectation is incomplete or wrong, a green result provides false confidence.

This problem predates generative AI. AI makes it more visible because the same model can generate both sides of the comparison.

If a model writes a function and then writes a test based on its own interpretation, the test may confirm internal consistency rather than external correctness. A generated test report may accurately state which generated tests passed while saying nothing about whether the right tests were selected.

Pass rate, test count, and code coverage must not be confused with quality assurance. Coverage shows which code executed. It does not prove that assertions were meaningful, requirements were correct, or missing risks were discovered.

## When AI can modify the test

The risk increases when the implementation agent can also edit test code.

To make a failing suite pass, it may weaken an assertion, remove a difficult case, update an expected result, regenerate a snapshot, or replace a real dependency with a simple mock.

This does not require deliberate deception. If the completion signal is “make all tests pass,” modifying the test can look locally rational.

Mocks are not the problem. They are essential for fast, isolated, deterministic feedback. The problem is treating mocked success as evidence that real databases, networks, services, concurrent workloads, and production data will behave the same way.

Quality needs a portfolio of evidence: isolated tests, contract tests, real integration tests, selected E2E journeys, non-functional verification, and production feedback.

## How to ensure the quality of AI-generated software

AI should not simultaneously be the requirements author, implementer, test designer, and final judge.

AI-generated software needs independent evidence outside the implementation agent's immediate optimization loop.

### Humans own critical rules and risks

Accountable stakeholders must identify business invariants, safety constraints, regulatory obligations, abuse cases, and unacceptable outcomes. AI can expand the list, but it should not silently decide what matters.

### Protect acceptance evidence

Critical acceptance tests, security policies, and release thresholds should not be freely editable by the agent responsible for passing them. Changes need review and an audit trail.

### Test real integrations

Mocks should be complemented by contract verification and tests using real databases, queues, identity systems, services, and production-like infrastructure.

### Apply systematic test design

Teams should explicitly use boundary-value analysis, equivalence partitions, decision tables, state transitions, negative tests, concurrency tests, failure injection, and historical incident replay instead of relying only on cases the model volunteers.

### Verify non-functional quality

Performance, security, reliability, recovery, accessibility, compatibility, observability, and maintainability need measurable requirements and independent evidence.

### Audit changes to tests

Changes to assertions, expected outputs, snapshots, mocks, exclusions, and baselines are quality-relevant events. Ask not only “Did the tests pass?” but also “What changed in the tests, who changed it, and why?”

### Keep production feedback inside QA

No pre-release suite models every real condition. Monitoring, tracing, canary releases, feature flags, rollback, and incident learning remain part of quality assurance—not merely operations.

## Has QA disappeared?

QA was never only the execution of test cases. Its deeper role is to question assumptions, identify risks, define evidence, preserve independence, and determine whether a product is fit for use.

Those responsibilities become more important when implementation becomes faster.

If AI can generate a feature in minutes, the bottleneck moves from production to judgment. Teams must decide whether the requested behavior was correct, whether the evidence is trustworthy, which risks remain invisible, and who is authorized to accept them.

In the AI software era, has QA disappeared?

Can SDD truly ensure software quality?

Or have we simply not yet developed QA methodologies and tools that match how AI actually generates software?
