# Did AI Follow the Rule?

> Use decision evidence and risk signals to review behavior and improve the rules.

After using behavioral Rules in actual AI-assisted software development, the initial results looked promising.

The same Rules could be reused across development tasks.

I did not have to repeatedly explain the same constraints in every prompt.

Requirements, source-code generation, and test-related work could use different Rulesets while still drawing from the same Rule Library.

And subjectively, the generated documents and code appeared more consistent.

There seemed to be fewer unexpected changes.

The development process felt more controlled.

But that created an uncomfortable question:

> **How did I know the Rules were actually being followed?**

A better result did not prove that a Rule caused it.

A Rule being loaded into the context did not prove that the model followed it.

And a successful test did not prove that the AI respected the development constraints while producing the result.

I had reusable Rules.

I had a Rule Library.

I had a way to deliver Rules into development tasks.

But I still could not answer a basic governance question:

> **What actually happened when the AI made a development decision?**

---

## Better output did not prove that the Rule was followed

Consider a simple development constraint:

```text
AI MUST NOT modify test code
unless test modification is explicitly authorized.
```

Suppose I asked the AI to fix an implementation problem.

The tests passed afterward.

The source code looked correct.

The test files were unchanged.

It would be easy to conclude:

> The Rule worked.

But what did I actually know?

Perhaps the Rule influenced the decision.

Perhaps the model would not have modified the tests anyway.

Perhaps another instruction prevented the change.

Perhaps the Rule was never relevant to the decision.

The final artifact alone could not tell me.

This exposed an important distinction:

```text
Good Result
≠
Rule Compliance

Rule Loaded
≠
Rule Triggered

Rule Triggered
≠
Rule Followed
```

If I wanted to govern development behavior rather than simply hope that the Rules were useful, I needed visibility into the decisions made during development.

Fortunately, another part of the development system had already started moving in that direction.

---

## Decision Evidence already existed

Before this became a Rule-governance problem, I had already been working on preserving development decisions as evidence.

Instead of keeping only the final source code or document, the development process could record individual decision behavior.

A simplified evidence format looked like this:

```text
Decision Evidence

ID: {{task.id}}
Timestamp: {{task.timestamp}}
Author: {{task.author}}
Command: {{task.command}}
Mode: {{task.mode}}
Session Type: {{task.session_type}}

{{stage.name}} - {{decision.id}}

Decision Type: {{decision.type}}
Decision Point: {{decision.decision_point}}
Time: {{decision.timestamp}}
Impact Level: {{decision.impact_level}}
Status: {{decision.status}}

Context
{{decision.context}}

Input Artifacts
{{#each decision.input_files}}
- {{this}}
{{/each}}

Constraints
{{#each decision.constraints}}
- {{this}}
{{/each}}

Candidates Analysis

{{#each decision.candidates}}

Option: {{this.name}}

Pros:
{{#each this.pros}}
- {{this}}
{{/each}}

Cons:
{{#each this.cons}}
- {{this}}
{{/each}}

{{/each}}

Decision

Selected:
{{decision.selected_option}}

Rationale:
{{decision.rationale}}

Impact
{{decision.impact}}

Traceability

Trace IDs:
{{decision.trace_ids}}

Applicable Rules:
{{decision.rules}}
```

Originally, the important idea was simple:

> **Do not preserve only what was produced. Preserve the development decision that produced it.**

This gave me something the final artifact alone could not provide.

A source-code diff could tell me what changed.

Decision Evidence could preserve information about:

- what decision was being made,
- what context existed,
- what artifacts were considered,
- what alternatives were considered,
- what constraints were present,
- what option was selected,
- why it was selected,
- and what impact the decision was expected to have.

Once BRA Rules existed, this evidence structure became much more useful.

---

## Which Rule actually constrained this decision?

The evidence already had a concept of `Constraints`.

That created a natural connection.

Instead of merely knowing that a Ruleset had been loaded somewhere earlier in the workflow, each development decision could record the constraints relevant to that particular behavior.

Conceptually:

```text
Development Task
↓
Ruleset Loaded
↓
Decision Behavior
↓
Applicable / Triggered Constraints
↓
Decision Evidence
```

Now the evidence could preserve something like:

```text
Decision:
Modify implementation to satisfy authentication tests

Constraints:
- CODE-TI-01 v1.2
- CODE-AR-03 v1.0

Applicable Rules:
- CODE-TI-01
- CODE-AR-03
```

This changed what could be inspected later.

Before:

```text
Task
→ Ruleset
→ Result
```

After:

```text
Task
↓
Decision Behavior
├── Context
├── Constraints
├── Candidate Options
├── Selected Decision
├── Rationale
├── Impact
└── Applicable Rules
↓
Result
```

The relationship between Rule and behavior had become visible.

---

## This was the first governance infrastructure I actually needed

At this point, it would be tempting to say:

> Now I had governance.

But that would be too strong.

What I actually had was something more fundamental.

I had made the information required for governance **observable**.

Before Decision Evidence:

```text
AI Development
↓
Artifact
```

After Decision Evidence:

```text
AI Development
↓
Decision Behavior
↓
Evidence
↓
Artifact
```

And after connecting Rules to the evidence:

```text
Rule
↓
Decision Behavior
↓
Evidence
↓
Artifact
```

The system could now expose:

> What decision happened?

> What constraints were active?

> Which Rules were applicable?

> What option was selected?

> Why?

> What was the expected impact?

This was not governance itself.

It was the engineering work required **before governance could become practical**.

I think of this as making governance elements explicit.

Or more broadly:

> **Governance Observability Engineering.**

Governance cannot reliably inspect information that the engineering process never preserves.

Before deciding whether behavior is acceptable, the behavior first has to become visible.

[[M_BRA_A_05-0.png]]

---

## Then I encountered the second problem

Once development decisions were recorded, I discovered the opposite problem.

There was no longer too little information.

There was too much.

A single prompt could involve multiple development decisions.

A seemingly simple coding task might contain decisions about:

```text
Which file should change?

Which existing interface should be reused?

Should a function be extended or replaced?

Should a test be modified?

Should a dependency be introduced?

Which error-handling strategy should be used?

Does the requested change affect an existing requirement?

Is an architectural change necessary?
```

If every decision produced evidence, one task could generate many Decision Evidence records.

Across a development workflow, the volume increased quickly.

Conceptually:

```text
Prompt
↓
Decision 01
Decision 02
Decision 03
Decision 04
Decision 05
Decision 06
...
↓
Evidence 01
Evidence 02
Evidence 03
Evidence 04
Evidence 05
Evidence 06
...
```

I had solved the observability problem.

But I had created a review problem.

---

## Evidence that nobody can review is not practical governance

The obvious solution would be:

> Review every Decision Evidence record.

That sounds rigorous.

It is also operationally unrealistic.

Imagine a development session producing dozens of decisions.

Then multiply that by:

```text
Developers
×
Tasks
×
Sessions
×
Development Stages
×
Projects
```

The result is not better governance.

It is an evidence backlog.

And if governance requires someone to manually inspect every AI decision, the governance mechanism itself becomes a development bottleneck.

The problem therefore changed again.

Originally:

> How do I know what the AI decided?

Decision Evidence addressed that.

Now:

> **Which decisions actually require governance attention?**

That question connected this work to another part of my research: **Decision Risk**.

---

## Review should start from risk, not from evidence volume

My Decision Risk work examined another question:

> Which development decisions deserve attention because their effects may extend beyond the expected decision boundary?

That provided a different way to use Decision Evidence.

Instead of:

```text
Evidence
↓
Review Everything
```

the flow could become:

```text
Observe Decision
↓
Detect Risk
↓
Locate Relevant Evidence
↓
Review That Decision
```

This changed the economics of governance.

Evidence could remain comprehensive enough to preserve what happened.

But human attention did not have to be comprehensive.

The review process could become selective.

Conceptually:

```text
Many Development Decisions
          │
          ▼
    Risk Observation
          │
     ┌────┴────┐
     │         │
 No Signal   Risk Signal
     │         │
     │         ▼
     │    Retrieve Evidence
     │         │
     │         ▼
     │    Governance Review
     │
     ▼
Continue
```

The Decision Risk work is documented separately here:

https://papers.ssrn.com/sol3/papers.cfm?abstract_id=6655398

The important connection for BRA was not that Decision Risk became part of the Rule.

It did not.

The important connection was that **risk provided a reason to inspect a particular Decision Evidence record**.

---

## Evidence is not governance

This distinction became increasingly important.

It is easy to build a system that records everything and call it governance.

But recording is not governing.

Consider:

```text
Decision
↓
Evidence Stored
```

Nothing in that sequence determines whether anyone should care about the decision.

Nothing determines whether the Rule was effective.

Nothing causes a Rule to be reviewed.

Nothing causes a governance action.

Evidence provides observability.

Governance requires a reason to evaluate and potentially act.

The pattern that emerged was closer to:

```text
Decision Behavior
↓
Evidence

Decision Behavior
↓
Risk Observation
↓
Risk Signal
↓
Retrieve Relevant Evidence
↓
Review
↓
Governance Action
```

This was the point where I would say **development Rule governance** actually began.

Not when the evidence existed.

But when a governance signal could lead back to the relevant evidence and support a decision about the Rule or the development behavior.

---

## A concrete example

Suppose a task was intended to modify source code.

An applicable Rule constrained test modification.

During execution, the AI made several decisions.

Most were routine:

```text
Decision 01
Reuse existing helper function

Decision 02
Add null handling

Decision 03
Modify authentication logic

Decision 04
Modify test expectation

Decision 05
Update error mapping
```

Recording five evidence objects is possible.

Manually reviewing all five every time is expensive.

But suppose Decision 04 produces a risk signal because its effect reaches test code while the task authority was focused on source-code correction.

Now the workflow becomes:

```text
Decision 04
↓
Risk Observed
↓
Retrieve Decision Evidence
↓
Inspect Constraints

CODE-TI-01 v1.2

↓
Inspect Context
↓
Inspect Candidate Analysis
↓
Inspect Selected Decision
↓
Inspect Result
```

Now the reviewer is not searching blindly through a session.

The risk identifies the decision worth inspecting.

The evidence reconstructs the relevant decision state.

The Rule identifies the expected behavioral constraint.

Together they make governance review practical.

---

## Then something unexpected happened

The purpose of this mechanism was initially to determine whether AI behavior was respecting the Rules.

But once I started reviewing the evidence, the evidence also exposed problems in the Rules themselves.

Some Rules looked clear when written in isolation.

They became less clear when applied to actual development decisions.

A semantic boundary might be too broad.

A condition might be ambiguous.

A normative expression might constrain more behavior than intended.

Two Rules might interact in a way that was not obvious when each was reviewed independently.

The evidence was no longer only telling me:

> The AI did something questionable.

Sometimes it was telling me:

> **The Rule itself needs to be improved.**

---

## A Rule can be followed and still need revision

This is where Rule governance became different from simple compliance checking.

Suppose a Rule is:

```text
AI MUST NOT modify an artifact
outside the current task scope.
```

It sounds reasonable.

But repeated Decision Evidence might reveal that "current task scope" is interpreted differently across development situations.

Perhaps the Rule needs a more precise target.

Perhaps its condition needs refinement.

Perhaps its semantic relationship with another Rule is unclear.

The important point is that this is no longer hypothetical analysis of the Rule text.

There is now evidence from actual use.

The sequence becomes:

```text
Rule v1.0
↓
Used in Development
↓
Decision Behavior
↓
Risk Signal
↓
Evidence Review
↓
Semantic Problem Found
↓
Rule Revised
↓
Rule v1.1
```

That is a very different process from simply editing a prompt because an output looked wrong.

---

## The version number finally mattered operationally

Earlier, Rule versions were part of the Rule's governance structure.

Versioning made sense architecturally.

But once evidence began referring to actual Rule versions, versioning became operationally important.

Suppose:

```text
Decision Evidence A
→ CODE-TI-01 v1.1

Decision Evidence B
→ CODE-TI-01 v1.2
```

Now I can distinguish behavior produced under different Rule semantics.

If the Rule changes, old evidence still refers to the Rule that actually existed at that time.

That means:

```text
Rule Revision
≠
Rewrite History
```

The previous Rule version remains part of the historical decision context.

This is important because otherwise a later Rule update could make old evidence misleading.

The evidence must answer:

> **Which Rule did this decision actually operate under?**

Not:

> What does the Rule say today?

---

## Governance information also started changing

The semantic Rule was not the only thing that sometimes needed adjustment.

Actual use could also reveal that governance information needed to evolve.

For example:

```text
Applicability Context
Owner
Intent
Review Information
Governance Impact
Evidence Expectations
```

The important point was not that every Rule needed every possible governance field.

It was that the abstract governance surface created earlier could now absorb information learned from actual operation.

The direction became:

```text
Rule Definition
↓
Use
↓
Observe
↓
Risk
↓
Evidence Review
↓
Learn
↓
Update Rule Semantics
and/or
Update Governance Information
↓
New Version
```

Now the governance structure was no longer merely future-proof metadata.

It had become part of the Rule lifecycle.

---

## This was the point where Rule PDCA became real

It would have been possible to describe Rule governance as a PDCA process from the beginning.

But that would have been mostly conceptual.

The actual loop only became meaningful after all of these pieces existed.

First:

```text
Rule Library
```

Then:

```text
Rule Usage
```

Then:

```text
Decision Evidence
```

Then:

```text
Risk Observation
```

Then:

```text
Evidence Review
```

And finally:

```text
Rule Revision
```

Only then did a real feedback loop exist.

---

## PLAN

Define the behavioral Rule.

Validate it.

Assign its version and governance information.

Publish it to the Rule Library.

```text
Rule Definition
↓
Validation
↓
Rule Library
```

---

## DO

Use the Rule in actual AI-assisted development.

```text
Development Task
↓
Resolve Rules
↓
AI Development
↓
Decision Behavior
```

The important part is that actual behavior now creates evidence.

---

## CHECK

Do not manually inspect every decision.

Observe development decisions for risk.

When a risk signal appears:

```text
Risk Signal
↓
Locate Decision
↓
Retrieve Evidence
↓
Inspect Triggered Constraints
↓
Inspect Applicable Rule Version
↓
Review Decision Behavior
```

Now the review has a reason, a target, and evidence.

---

## ACT

The result of review may be:

```text
No Rule Problem
→ retain current Rule

Rule Semantic Problem
→ revise normative expression

Applicability Problem
→ revise relevant Rule information

Governance Problem
→ update governance information

Obsolete Rule
→ deprecate / supersede
```

If the Rule changes:

```text
Rule v1.2
↓
Review Evidence
↓
Revision
↓
Rule v1.3
↓
Rule Library
```

The next development task uses the new version.

The cycle continues.

---

## The actual loop was therefore not “Rule → Evidence”

It was:

```text
Rule
↓
Development Behavior
↓
Decision Evidence
↓
Risk Observation
↓
Selective Evidence Review
↓
Rule Evaluation
↓
Rule Revision
↓
New Version
↺
```

This distinction matters.

Without Evidence:

> Governance has nothing reliable to inspect.

Without Risk:

> Governance may have too much to inspect.

Without Review:

> Evidence remains stored information.

Without Rule Revision:

> Review does not create a learning loop.

Only when these pieces connect does the system begin to support continuous Rule governance.

[[M_BRA_A_05-1.png]]

---

## From governance visibility to governance action

Looking back, there were really two separate engineering problems.

The first was **visibility**:

> How can the development process expose the information governance would need?

Decision Evidence addressed that.

```text
Decision Behavior
↓
Explicit Context
Explicit Constraints
Explicit Candidates
Explicit Decision
Explicit Impact
Explicit Traceability
```

This made governance elements observable.

But observability alone created too much information.

The second problem was **attention**:

> Which observable decisions deserve governance review?

Decision Risk provided a way to narrow that space.

```text
Observable Decisions
↓
Risk
↓
Selected Evidence
↓
Review
```

Only after both existed could development Rule governance become practical.

---

## What changed in BRA?

Interestingly, this process did not require turning BRA into a governance engine.

BRA still defined behavioral Rules.

The Rule Library still stored them.

Skills or other mechanisms still delivered them.

Decision Evidence existed outside the Rule.

Decision Risk existed outside the Rule.

Review existed outside the Rule.

But they could now connect through Rule identity and version.

```text
                    Rule Library
                         │
                    Rule v1.2
                         │
                         ▼
Development Task → Decision Behavior
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
         Risk Observation      Decision Evidence
              │                     │
              └──────────┬──────────┘
                         ▼
                       Review
                         │
                         ▼
                  Rule Adjustment
                         │
                         ▼
                    Rule v1.3
                         │
                         └──────────────↺
```

That was enough.

The Rule did not need to own the whole governance process.

It only needed to be identifiable, versioned, traceable, and governable.

---

## From reusable Rules to governable Rules

At the beginning of this series, my problem was much simpler.

I wanted to stop repeating the same AI instructions.

That produced reusable Rules.

Then I needed to define what a Rule actually was.

Then I needed to structure, classify, store, and compose Rules.

Then I needed practical ways to use them during development.

But actual use exposed a final difference:

```text
Reusable Rule
≠
Governed Rule
```

A reusable Rule can be applied many times.

A governed Rule has something more:

```text
Rule
↓
Usage
↓
Observable Behavior
↓
Evidence
↓
Risk-triggered Review
↓
Revision
↓
Version History
```

That was the point where the Rule stopped being only a reusable AI constraint.

It became an engineering asset that could be observed, evaluated, corrected, and improved through actual development experience.

And that was the point where **development Rule PDCA** became real.

Behavior Rule Architecture · 05 / 06

#ArtificialIntelligence #AIGovernance #SoftwareEngineering #ResponsibleAI #RiskManagement



