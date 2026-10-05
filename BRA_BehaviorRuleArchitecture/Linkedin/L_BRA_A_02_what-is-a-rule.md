# What Is a Rule?

### From natural-language instructions to a structured definition of AI behavior

[[L_BRA_A_02-0.png]]

In the previous part, I described how AI instructions gradually moved out of prompts.

They became reusable instructions.

Then rule lists.

Then rulesets.

But that created another problem I had not really solved:

> **What exactly is a Rule?**

At that point, calling something a “rule” did not make it one.

A sentence in a prompt could be called a rule.

A coding guideline could be called a rule.

A project instruction could be called a rule.

A restriction could be called a rule.

Even a preference could be called a rule.

They all looked similar when written as natural language.

But they did not mean the same thing.

That became the next problem.

Looking back, I can trace this problem to **January 2026**, when I was trying to turn repeated AI development instructions into reusable Rules and Rulesets. Once those instructions were separated from prompts, I still had to determine what made one statement a Rule rather than a preference, policy, or constraint.

Each clarification solved one semantic ambiguity, but the underlying issue remained: natural-language instructions could look similar while expressing different levels of obligation and prohibition.

At the time, I was not yet defining the final architecture. I was trying to understand what a Rule had to mean before it could become a reusable engineering artifact.

---

## The scope at the time was software development

There is an important historical boundary to make clear before going further.

The problems described here emerged from **AI-assisted software development**, particularly the stage where AI was being instructed to create or modify development artifacts such as source code, tests, and documents.

I was not trying to design a universal rule language for every AI system or every domain.

The immediate questions were much more practical:

How do I tell AI what it must do while developing software?

How do I tell it what it must not change?

How do I reduce reinterpretation when the same development instruction is reused?

How do I make those instructions stable enough to use repeatedly?

Some of the concepts that emerged from this work can later be applied beyond software development, to other execution stages or domains.

But that was not where they started.

They started with software development problems.

---

# Problem 1: Moving instructions out of prompts did not remove interpretation

Moving instructions from prompts into reusable files solved one problem:

**location and reuse.**

It did not solve interpretation.

Consider these development instructions:

> Please avoid changing unrelated code.

> You should not change unrelated code.

> Do not change unrelated code.

> You must not change unrelated code.

A human can immediately see that they point in roughly the same direction.

But they do not carry exactly the same normative force.

And for an AI system, there was another issue.

Before following any of them, the model still had to interpret the sentence.

What is the action?

What is the target?

Is this a preference?

A recommendation?

A requirement?

A prohibition?

What counts as “unrelated”?

Moving natural language from a prompt into a Rule file did not remove those questions.

It only moved the ambiguity somewhere else.

So I started looking at the language itself.

---

# Problem 2: Natural-language sentence structure was too free

Natural language is useful because it is expressive.

That is also what makes it difficult to control.

The same software-development instruction can be written in many forms:

> When modifying the source code, please make sure existing tests continue to work.

Or:

> Existing tests should remain valid after source code changes.

Or:

> Source code changes must preserve existing test behavior.

The intent may be similar.

The structure is not.

If I wanted AI to decompose development instructions consistently, I first needed to reduce how much structural interpretation was required.

That led to **NNL — Normative Natural Language**.

NNL was not intended to eliminate natural language.

It was an attempt to make important instructions structurally clearer while keeping them readable by humans.

Conceptually, I was moving toward something like:

```text
Actor
+
Normative Expression
+
Action
+
Target
+
Condition
```

Instead of allowing every instruction to take an arbitrary linguistic form, the sentence itself could expose more of its structure.

The response to this problem was therefore not yet a Rule architecture.

It was much smaller:

> **Structure the sentence before asking AI to interpret it.**

NNL reduced one source of ambiguity.

But once sentence structure became clearer, another problem became easier to see.

---

# Problem 3: Structured sentences could still carry different normative meanings

Even with clearer sentence structure, the normative vocabulary was still wide open.

People naturally write things like:

```text
can
cannot
want
do not want
should
should not
need to
have to
must
must not
```

These words do not carry the same force.

Consider:

> AI should preserve existing tests.

and:

> AI must preserve existing tests.

Those are not equivalent.

The first can reasonably be interpreted as a recommendation.

The second expresses an obligation.

The problem becomes even clearer with:

> AI can modify the file.

Does that mean permission?

Capability?

Possibility?

A description of what the system is technically able to do?

The sentence may now be structurally clearer while its normative meaning remains ambiguous.

The next response was therefore to constrain not only the structure of the sentence, but also its vocabulary.

That led to **CNL — Constraint Normative Language**.

The progression was:

```text
Natural Language
        ↓
Constrained Sentence Structure
        ↓
NNL
        ↓
Constrained Normative Vocabulary
        ↓
CNL
```

NNL addressed structural variation.

CNL addressed normative variation.

---

# Problem 4: Too many normative expressions still required interpretation

CNL reduced the vocabulary, but another problem remained.

Every additional normative expression created another distinction that either the AI or the surrounding system had to interpret.

Expressions such as:

```text
CAN
CAN NOT
WANT
WANT NOT
```

were not useful enough as authoritative behavioral constraints.

Even recommendation-oriented expressions created another question:

> If a development rule says SHOULD, when is the AI allowed not to follow it?

That distinction may be useful in other kinds of specifications.

But for the development behavior I was trying to control, it introduced another interpretation point.

The objective was narrower:

> **Make required and prohibited behavior explicit.**

So the vocabulary continued to shrink.

Eventually, two expressions became the most important:

```text
MUST
MUST NOT
```

This created a much simpler normative distinction:

```text
MUST
→ required behavior

MUST NOT
→ prohibited behavior
```

And from that distinction, two concepts became useful:

```text
Policy
→ what must happen

Constraint
→ what must not happen
```

A Contract, when it restricts permitted development behavior, belongs on the **Constraint** side in this model.

The important transition was that the question changed from:

> What does this instruction probably mean?

toward:

> **What behavior is explicitly required or prohibited?**

[[L_BRA_A_02-1.png]]

---

# Problem 5: MUST and MUST NOT still did not make a rule executable

There was an important limitation.

Writing:

> AI MUST NOT modify unrelated source code.

does not magically make the instruction executable.

`MUST NOT` is still text to an LLM.

Capitalizing the words does not create enforcement.

It does something more limited, but useful:

> **It makes normative polarity explicit enough to represent independently.**

Instead of asking a model to infer whether something is a preference, recommendation, obligation, or prohibition, the intended polarity is exposed directly.

This distinction later became useful for engineering and governance.

But at this stage, it did not solve enforcement.

And that was acceptable.

The problem I was trying to solve at this point was not yet:

> How can a system deterministically enforce this Rule?

It was:

> **How can I represent the intended development behavior without repeatedly asking AI to infer its normative meaning?**

That narrower problem needed to be solved first.

---

# Problem 6: Normative polarity did not tell me what behavior was being governed

Knowing that something was required or prohibited was still not enough.

One recurring development situation made this particularly visible.

Suppose I asked AI to fix an implementation and make the existing tests pass.

The intended solution was:

```text
Source Code
↓
Fix implementation
↓
Existing Tests Pass
```

But the objective visible to the AI could effectively become:

> **Make the tests pass.**

If the test files were also available for modification, another solution existed:

```text
Source Code
+
Test Code
↓
Modify whichever makes the failure disappear
↓
Tests Pass
```

In practice, this meant AI could modify the test itself—changing an assertion, expected value, fixture, or test condition—so that the test passed without actually correcting the intended implementation behavior.

From the AI's perspective, this could still satisfy the immediate observable objective.

From an engineering perspective, it was the wrong solution.

So simply saying:

> Fix the code and make the tests pass.

was not enough.

I needed to state not only the desired outcome, but also what the AI was **not allowed to modify** while achieving it.

That made a statement like this useful:

> **AI MUST NOT modify test code when fixing source code unless test modification is explicitly authorized.**

Its structure could be decomposed into:

```text
MUST NOT
+
modify
+
test_code
```

Now the pieces had distinct meanings:

```text
MUST NOT
→ normative polarity

modify
→ governed action

test_code
→ governed target
```

This was important because the problem was not simply that the AI had generated incorrect code.

The AI had found a path to the requested outcome through an artifact that I did not intend to be part of the modification space.

That made **Target** explicit.

Other Targets followed naturally:

```text
document
source_code
test_code
configuration
```

And Actions could also be separated:

```text
create
update
fix
refactor
```

A development instruction was beginning to look less like an arbitrary sentence and more like a structured behavioral statement:

```text
Normative
+
Action
+
Target
```

This solved one ambiguity.

But making Target explicit exposed another problem almost immediately.

---

# Problem 7: Every new Target seemed to require another Rule

Once Target became explicit, the Rule became easier to understand.

But it also became easier to duplicate.

Suppose the intended behavior was essentially:

> Do not modify artifacts outside the requested change.

I could write:

```text
AI MUST NOT modify unrelated source_code.
```

Then:

```text
AI MUST NOT modify unrelated test_code.
```

Then:

```text
AI MUST NOT modify unrelated document.
```

Then configuration.

Then schema.

Then scripts.

Then deployment files.

The behavioral principle had not really changed.

Only the affected Target had changed.

That created a scaling problem:

> **If every Target requires another copy of the same Rule, how many Rules will I eventually need?**

As development artifacts increased, the Rule set could grow simply because the same behavioral requirement had been repeated for different Targets.

That did not feel like a new Rule every time.

It felt like the **same Rule applied somewhere else**.

This distinction became important.

---

# Problem 8: The Rule and where the Rule applies were not the same thing

This was the point where another separation started to become necessary.

Consider the behavioral statement:

> AI MUST NOT modify unrelated artifacts.

The normative behavior can remain stable.

What changes is where that behavior applies.

Conceptually:

```text
Rule
AI MUST NOT modify unrelated artifacts
```

could apply to:

```text
source_code
test_code
document
configuration
```

Instead of creating four independent behavioral meanings, I could begin thinking about:

```text
Rule
+
Applicable Target
```

The question was shifting from:

> What does this Rule say?

to a second question:

> **Where does this Rule apply?**

That distinction helped prevent Rule proliferation.

Instead of encoding every combination directly into a new Rule:

```text
Rule × Target
Rule × Target
Rule × Target
Rule × Target
```

the behavioral statement and its applicability could begin to separate:

```text
              Rule
               │
      ┌────────┼────────┐
      ↓        ↓        ↓
 source_code test_code document
```

This was still an early engineering response to a practical development problem.

I was not yet starting from a formal theory of Scope or Boundary.

But an important idea had appeared:

> **A Rule can remain stable while its applicable range changes.**

That idea would matter much more later.

---

# Problem 9: Target alone could not fully describe where a Rule applied

Once I started separating a Rule from its applicable Target, another limitation became visible.

Target was only one dimension.

The same Rule might apply differently depending on:

- who is acting,
- what action is being performed,
- which artifact is affected,
- which development stage is active,
- or which context the execution belongs to.

The test-code example already hinted at this.

The useful constraint was not necessarily:

> AI can never modify test code.

That would be too broad.

There are legitimate tasks where modifying tests is exactly what AI is supposed to do.

The actual question was closer to:

> **When AI is fixing source code against an existing test, is test code inside or outside the permitted modification range?**

The answer depends on context.

The same `test_code` Target could therefore be:

```text
Fix implementation
→ test_code modification not applicable / not authorized

Update obsolete test
→ test_code modification applicable

Create new feature tests
→ test_code modification applicable
```

So Target alone could not determine whether a Rule applied.

The problem had expanded from:

> Which Target does this Rule affect?

to:

> **Under what conditions is this Rule applicable?**

At that time, this was still an applicability problem arising from software-development Rule reuse.

Later work would separate and formalize related ideas much further through **Scope** and **Boundary**.

Those later concepts should not be projected backward as if they already existed here in their final form.

But the engineering question was already visible:

```text
Rule
↓
Action + Target
↓
Different tasks change what is applicable
↓
Applicability
↓
Where does this Rule actually apply?
```

That question would eventually become much larger than Rule design itself.

---

# Problem 10: I was calling things “Rules” before I could define what a Rule was

Earlier, I had already been using rule lists and rulesets.

But “Rule” was still close to:

> an instruction that should be reused.

That was operationally useful.

Conceptually, it was weak.

After working through sentence structure, normative vocabulary, behavioral polarity, action, target, and applicability, the meaning started to become narrower.

A Rule was becoming:

> **a structured statement describing required or prohibited behavior, separated from the conditions under which that behavior applies.**

In the development context I was working with, two different questions were beginning to emerge:

```text
What behavior is required or prohibited?
                ↓
               Rule

Where does that Rule apply?
                ↓
          Applicability
```

This separation was important.

Without it, every new context risked becoming another Rule.

The conceptual progression therefore looked more like this:

```text
Natural Language
        ↓
Structured Natural Language
        ↓
NNL
        ↓
Controlled Normative Vocabulary
        ↓
CNL
        ↓
MUST / MUST NOT
        ↓
Policy / Constraint
        ↓
Action + Target
        ↓
Rule
        ↓
Target proliferation
        ↓
Applicability
```

This was not one design decision.

Each concept appeared because the previous representation exposed another unresolved problem.

```text
Sentence structure was too free
→ NNL

Normative vocabulary was too broad
→ CNL

Normative force was still ambiguous
→ MUST / MUST NOT

Required and prohibited behavior needed distinction
→ Policy / Constraint

The governed behavior was unclear
→ Action + Target

Target-specific Rules started multiplying
→ Applicability

Target alone was insufficient
→ broader applicability dimensions
```

This was becoming more than a language problem.

[[L_BRA_A_02-2.png]]

---

# Problem 11: An instruction could be reused, but its meaning could still be reconstructed differently

This became the deeper distinction between an instruction and the emerging Rule concept.

An **instruction** can depend heavily on interpretation.

Its intended behavior may need to be reconstructed every time another model, session, or workflow consumes it.

A **Rule**, as I was beginning to define it, should expose enough of that meaning structurally that the behavioral intent does not need to be reconstructed from scratch every time.

And increasingly, another principle was becoming visible:

> **The Rule should not have to change merely because the context in which it applies changes.**

That does not mean the Rule is automatically enforceable.

It does not mean an LLM will always obey it.

It does not mean the Rule itself decides whether execution is allowed.

And it does not mean this representation is limited forever to software development.

Those are separate questions.

At this stage, the objective remained deliberately narrow:

> **Make intended development behavior explicit enough to become a stable and reusable engineering object, while separating that behavior from where it applies.**

Once that became possible, however, a completely different class of problems appeared.

---

# Problem 12: Once Rules became reusable, language was no longer the main problem

If I have one Rule, I can simply read it.

But once I have dozens of Rules, new questions appear:

How do I identify one?

What happens when it changes?

Which version was used?

Who is supposed to follow it?

When does it apply?

Who owns it?

Why does it exist?

Where did it come from?

What happens when two Rules are used together?

These are no longer primarily language problems.

They are engineering-object problems.

And one of those questions—

> **When does this Rule apply?**

—would eventually grow into a much larger investigation of Scope and Boundary.

But first, the Rule itself needed to become a manageable engineering object.

The problem had moved from:

> **What does a Rule mean?**

to:

> **How should a Rule exist inside a software-development system?**

That became the next step in the evolution of Behavior Rule Architecture.

**LBRA-03: When a Rule Became an Engineering Object**

#BehaviorRuleArchitecture #BehaviorRules #AIEngineering #SoftwareEngineering
