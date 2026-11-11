# How Do You Ensure the Quality of AI-Generated Code?

“All tests passed.”

For decades, this sentence has been used as evidence that software is ready. In AI-assisted development, however, it can hide a new problem: the implementation, the tests, and the explanation of the results may all come from the same source.

Do you review AI-generated code?

Do you ask AI to produce a test report—and then audit that report?

Do you independently run the test code yourself to verify the result?

These questions are not about distrusting AI. They are about understanding what software quality evidence can—and cannot—prove.

## The question that started this investigation

At first, I thought the reason a Vibe Coding application could pass every test and still be unusable was straightforward: its tests often covered only the user interface and a few end-to-end happy paths. Exceptions, data boundaries, operational failures, and real execution environments were largely absent.

Then I wondered whether a more structured approach would solve the problem. What if non-functional requirements were included from the beginning? What if Specification-Driven Development, or SDD, included explicit test specifications? Could that provide a reliable quality guarantee for AI-generated code?

While organizing my thoughts on edge cases, I encountered a deeper limitation. AI can generate familiar boundary cases, invalid inputs, and exception tests. But unless it receives the relevant business rules, data constraints, risk models, production history, and past incidents, it can test only what can be inferred from the context it has been given.

It cannot prove that every important scenario has been identified.

That changes the question. The issue is no longer simply whether we have enough tests. It is:

**Who defines the correct result, and how do we know that the test itself is correct?**

## A brief history of software quality evidence

Software testing has never been one single activity. Different practices emerged to answer different quality questions.

In many traditional or regulated projects, quality evidence was expressed through formal artifacts. A Qualification Test Report, or QTR, documented whether a system satisfied defined qualification requirements. An Acceptance Test Report, or ATR, recorded whether the delivered system met the conditions for customer or organizational acceptance.

As Agile practices became common, teams increasingly used acceptance criteria to describe when a backlog item or feature should be considered complete. But acceptance criteria did not replace test reports. They serve a different purpose.

- Acceptance criteria define the conditions for accepting a requirement.
- Test reports document what was tested, what passed or failed, which defects remain, and what risks are known.

Agile projects subject to regulatory, contractual, safety, or audit obligations still need test records and evidence. The format may change, but the need for traceability does not disappear.

The history of software development methods also introduced several approaches that are sometimes incorrectly treated as successive replacements.

### TDD: feedback at the implementation level

Test-Driven Development begins with a failing test. The developer writes the minimum implementation required to make it pass, then refactors the code while preserving behavior.

TDD is often associated with unit or component testing because it provides fast feedback close to the implementation. But its essential contribution is not a particular test level. It is the use of executable examples to guide design and provide a regression safety net.

TDD can show that the implementation behaves as the developer expected. It cannot independently establish that the expectation represents the complete business need.

### ATDD: shared agreement before implementation

Acceptance Test-Driven Development moves the conversation toward business outcomes. Business representatives, developers, and testers collaborate before implementation to define acceptance examples.

ATDD is not simply another name for end-to-end testing. An acceptance example may be implemented at a service, API, component, or user-interface level. Its value lies in establishing shared understanding before code is written.

### BDD: behavior expressed through a shared language

Behavior-Driven Development emphasizes collaboration and describes system behavior using language that business and technical participants can understand together.

Given–When–Then is a common format:

- Given describes the initial context.
- When describes an action or event.
- Then describes the expected outcome.

But BDD is more than a sentence template, and it is not limited to end-to-end tests. Its purpose is to make assumptions and behavior discussable before they are embedded in code.

TDD, ATDD, and BDD can coexist. They operate at different points in the conversation between intent, behavior, implementation, and evidence.

## Three propositions about the direction of AI-assisted testing

The history above suggests three propositions that matter when software is generated by AI.

### 1. The center of attention has moved toward visible business behavior

TDD, ATDD, and BDD should not be described as a linear sequence in which one replaced another. TDD remains closely associated with implementation-level feedback, while ATDD and BDD bring testing language closer to business requirements and observable acceptance behavior.

Nevertheless, the broader direction of modern software delivery has increasingly emphasized what stakeholders can describe and observe: user journeys, acceptance criteria, examples, and externally visible outcomes. This is valuable because it aligns development with business intent. But it can also move attention away from less visible engineering concerns found closer to the code: internal invariants, exception paths, numerical boundaries, resource handling, concurrency, data corruption, and failure recovery.

A feature may therefore satisfy its visible acceptance examples while remaining weak at the engineering level. Business-facing behavior and implementation-level correctness are complementary forms of evidence; one cannot replace the other.

### 2. SDD often functions as an AI contract between a prompt and a formal specification

In practice, many forms of Specification-Driven Development sit somewhere between Vibe Coding and a complete formal specification. The specification acts as an AI contract: it preserves intent, constraints, tasks, and acceptance conditions so that an agent has something more stable than a conversational prompt.

This is an important improvement. It reduces ambiguity, preserves context, and makes generated work easier to trace. Yet its center of gravity often remains at the requirement and observable-behavior level. It describes what the user expects to see more readily than every internal property the implementation must preserve.

Unless engineering constraints are made explicit, an SDD workflow may still omit internal invariants, resource limits, concurrency behavior, migration safety, rollback conditions, observability, and failure semantics. The AI contract is only as complete as the engineering knowledge encoded within it.

### 3. AI-generated tests are inferred tests, not proof of engineering correctness

When AI adds tests by itself, it infers them from the prompt, specification, existing code, nearby tests, and familiar testing patterns. These are **inferred tests**: plausible examples derived from the context available to the model.

They may be useful, and some may reveal real defects. But they are not automatically **engineering-correctness tests**. Such tests require an independent basis for deciding what must always hold: architecture rules, domain invariants, threat models, interface contracts, numerical properties, operational limits, historical failures, or validated expectations from accountable stakeholders.

If AI infers both the implementation and its tests from the same context, a passing result primarily demonstrates consistency between generated artifacts. It does not, by itself, demonstrate correctness against the parts of engineering reality that were never present in that context.

## Test levels are not the same as test types

Discussions about quality often mix together test levels, test types, techniques, and development methods. The distinctions matter because each reveals a different class of risk.

Common test levels include:

### Unit or component testing

This verifies an individual function, class, module, or component in isolation. It provides fast and precise feedback but normally uses controlled inputs and substitutes for external dependencies.

### Component integration testing

This verifies the interaction between components inside a system. It can expose mismatched assumptions about data, state, sequencing, or error handling.

### System testing

This verifies the behavior and quality characteristics of the complete system. Functional and non-functional tests can both occur at this level.

### System integration testing

This verifies interfaces between the system and external systems or services. Authentication, message formats, timeouts, retries, compatibility, and failure recovery become important here.

### Acceptance testing

This determines whether the system satisfies business needs and is ready for delivery, deployment, or operational use.

End-to-end testing is related but should not be treated as an exact synonym for system or acceptance testing. An E2E test follows a complete user or business flow from beginning to end, potentially crossing several systems. It proves that a selected journey works under selected conditions—not that every relevant quality risk has been addressed.

Test types answer a different question: what quality characteristic are we evaluating?

- Functional testing asks whether the required functions are complete, correct, and appropriate.
- Non-functional testing examines performance, security, reliability, usability, compatibility, maintainability, and other quality characteristics.
- Structural testing examines internal paths, branches, and coverage.
- Change-related testing confirms fixes and checks for regressions.

A system can pass functional tests and still be unusable because it is too slow, insecure, unreliable, inaccessible, or impossible to operate safely.

## Quality is more than functional correctness

Software quality can be considered through at least three perspectives.

### Functional correctness

Does the software do what the specification says?

### Non-functional quality

How well does it behave? Is it secure, reliable, efficient, usable, compatible, maintainable, and resilient?

### Fitness for purpose

Does it solve the actual user and business problem?

The third question is especially important. A system can implement an incorrect specification perfectly. It can pass every automated test and still fail its users.

Non-functional requirements therefore need to be measurable. “The system must be fast” is difficult to verify. Better requirements define observable thresholds, such as:

- 95% of API requests must complete within 300 milliseconds.
- Recovery time after a service failure must not exceed 15 minutes.
- A user must be unable to read data belonging to another tenant.
- The error rate must remain below 0.1% under 10,000 concurrent connections.

Writing these conditions into a specification is valuable, but it is not the same as verifying them. Verification still requires suitable data, environments, tools, and release thresholds.

## Testing techniques fill different gaps

Several techniques complement the test levels and development methods described above.

Contract testing verifies that requests, responses, or messages exchanged between services conform to a shared contract. In Consumer-Driven Contract Testing, consumers express the interactions they depend on, and providers verify that those expectations remain supported.

Data-Driven Testing executes the same test with multiple combinations of inputs and expected outputs. It can be applied to unit, API, integration, and E2E testing.

Boundary-value analysis explores values at and around limits. Equivalence partitioning groups inputs expected to behave similarly. Decision tables examine combinations of conditions and outcomes. State-transition testing verifies how behavior changes as the system moves between states.

These techniques are important because examples generated from an obvious happy path rarely expose every hidden assumption.

## The AI-specific quality problem

AI introduces more than higher code volume. It changes the relationship between the producer of the code and the producer of the evidence.

Traditionally, a business analyst might define requirements, a developer implement them, a tester design independent cases, and a customer or product owner perform acceptance. The separation was never perfect, but multiple perspectives could challenge one another.

An AI coding agent may now:

1. interpret the requirement;
2. generate the implementation;
3. generate the test cases;
4. execute the tests;
5. modify failing code or tests;
6. produce the final test report.

This workflow is efficient, but it creates correlated error. If the original interpretation is incomplete, every downstream artifact may consistently reflect the same omission.

Imagine that a requirement fails to mention tenant isolation. The AI may generate an API that returns records correctly, tests that verify the returned records, and a report showing that all tests passed. The code and tests agree—but neither checks whether one tenant can access another tenant's data.

Consistency is not independence.

## When AI can change the test

The risk becomes greater when the same agent is authorized to modify both implementation and test code.

To make a failing suite pass, an agent might:

- weaken an assertion;
- remove a difficult or unstable case;
- update the expected result to match incorrect behavior;
- mock a real dependency that the test was intended to verify;
- replace a behavioral assertion with a check that no exception occurred;
- regenerate a snapshot or baseline without investigating why it changed.

These actions are not necessarily deliberate deception. The agent is optimizing toward the completion signal it has been given. If completion means “make all tests pass,” changing the test can appear locally rational.

Mocking itself is not the problem. Mocks are essential for fast, isolated, deterministic tests. The problem is allowing mocked success to stand as evidence that a real database, external service, network, concurrent workload, or production dataset will behave the same way.

Quality requires a portfolio of evidence: isolated tests for fast feedback, contract tests for service expectations, integration tests using real dependencies, and selected E2E tests for critical journeys.

## The test oracle problem

Every test needs an oracle: a way to determine whether the observed result is correct.

Tests can demonstrate that implementation behavior matches the expected result encoded in the test. If that expected result is wrong or incomplete, a green test provides false confidence.

This problem existed long before generative AI. AI makes it more visible because the same model can generate both sides of the comparison.

If a model writes a function and then writes a test based on its own interpretation of that function, the test may confirm internal consistency rather than external correctness.

The same issue affects generated test reports. A report can accurately summarize which generated tests passed while saying nothing about whether the right tests were chosen.

This is why test quantity, code coverage, and pass rate must not be confused with quality assurance. Coverage can show which code executed. It cannot prove that the assertions were meaningful, the requirements were correct, or the missing risks were discovered.

## Can SDD ensure software quality?

Specification-Driven Development is a valuable response to the ambiguity of prompt-driven coding. It treats a structured, persistent specification as the source of truth from which agents plan, implement, and verify software.

SDD can improve quality by making intent explicit, preserving constraints, connecting implementation to acceptance criteria, and reducing the loss of context across agent sessions.

But SDD cannot make a specification self-validating.

If the specification omits an edge case, the implementation and tests may omit it faithfully. If a non-functional requirement is vague, generated verification may also be vague. If the wrong stakeholder assumption becomes authoritative, automation can reproduce the mistake faster and more consistently.

SDD improves traceability between intent and output. It does not, by itself, prove that the intent is complete, correct, measurable, or fit for purpose.

## What AI-era quality assurance may require

AI-generated software needs evidence that is independent of the implementation agent's immediate optimization loop.

### Human ownership of risks and critical rules

Humans should identify business invariants, safety constraints, regulatory obligations, abuse cases, and unacceptable outcomes. AI can help expand the list, but accountable stakeholders must decide what cannot be violated.

### Protected acceptance evidence

Critical acceptance tests, security policies, and release thresholds should not be freely editable by the agent responsible for making the implementation pass. Changes should require review and leave an audit trail.

### Independent generation and adversarial review

Where practical, one process can generate the implementation while another generates challenges from a separate context, model, rule set, or risk catalog. A second AI is not automatically independent, but separation can reduce simple self-confirmation.

### Real integration environments

Mocks should be complemented by contract verification and tests against real databases, queues, identity systems, external services, and production-like infrastructure.

### Systematic test design

Teams should explicitly apply boundary-value analysis, negative testing, state transitions, decision tables, concurrency tests, failure injection, and historical incident replay instead of relying only on cases the model volunteers.

### Non-functional verification

Performance, security, reliability, accessibility, compatibility, observability, recovery, and maintainability require their own measurable requirements and evidence.

### Review of test changes

Organizations should treat modifications to assertions, expected outputs, snapshots, mocks, and test exclusions as security- and quality-relevant events. The important question is not only “Did the tests pass?” but also “What changed in the tests, and why?”

### Production feedback

Pre-release testing cannot model every real condition. Monitoring, tracing, canary releases, feature flags, rollback mechanisms, and incident learning remain part of quality assurance—not merely operations.

## Has QA disappeared?

AI can write code, generate tests, inspect failures, and produce reports. This may reduce some repetitive testing work, but it does not eliminate the quality function.

QA was never only the act of executing test cases. Its deeper role is to question assumptions, identify risks, define evidence, preserve independence, and determine whether a product is fit for use.

Those responsibilities become more important when implementation becomes faster.

If AI can generate a feature in minutes, the bottleneck moves from production to judgment. Teams must decide whether the requested behavior was correct, whether the evidence is trustworthy, which risks remain invisible, and who is authorized to accept them.

The future may therefore require more than applying traditional QA tools to AI-generated code. We may need an AI-specific quality discipline designed around correlated errors, editable tests, model uncertainty, incomplete context, and the speed at which agents can reproduce mistaken assumptions.

In the AI software era, has QA disappeared?

Can SDD truly ensure software quality?

Or have we simply not yet developed the QA methodologies and tools that match how AI actually generates software?
