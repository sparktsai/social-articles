## Relay 1 — Reply from the main account

Start with the boundaries that acceptance criteria rarely mention:

• counters that grow for years
• values the current business rules don’t recognize
• production volumes and combinations absent from test data

The expected path can pass while all three remain untested.

## Relay 2 — Reply from the main account

When humans wrote most of the code, we often added exception handling, negative tests, and error-path tests ourselves.

AI GenCode changes the bottleneck: code and E2E tests arrive faster, but review time does not.

More output can mean more unchecked assumptions.

## Relay 3 — Reply from the main account

I noticed this years ago while manually testing AI-generated code. I put together a small Robustness Testing Skill and still use it today.

It generates and runs edge-case unit tests, then gives me a report I can scan in about five seconds to decide what needs investigation.

## Relay 4 — Reply from the main account

The value is not “more tests.”

It is turning hidden assumptions into executable evidence before production data reaches them.

An untested edge case is not free. It may be a deferred incident, data repair, and emergency fix written into the code.

How do you detect yours?
