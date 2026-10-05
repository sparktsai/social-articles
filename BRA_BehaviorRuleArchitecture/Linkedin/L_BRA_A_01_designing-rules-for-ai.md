# When Did You Start Designing Rules for AI?

### Prompt? Code comments? CLAUDE.md? Or something else?

[[L_BRA_A_01-0.png]]

When did you start designing rules for AI?

Was it when you started writing longer prompts?

When you created a `CLAUDE.md` file?

When you added instructions directly into your source code?

Or did you never really think of them as "rules" at all?

For me, there wasn't a single moment when I decided:

> "I need a rule architecture."

It happened gradually.

Each step solved one problem, then exposed another.

---

## It Started with Prompt Engineering

Like many people working with AI-assisted development, I started with prompts.

Looking back, I can trace this problem to **July 2025**, while developing a document and knowledge management system. As the development work became more complex, I repeatedly had to bring earlier decisions and constraints back into the conversation.

Each correction solved the immediate problem, but the underlying issue remained: the AI could respond to the current request without consistently carrying forward every constraint established earlier in the development process.

At the time, I did not call these constraints "rules." They were simply additional instructions needed to keep the implementation aligned with the intended architecture.

At first, the instructions were simple.

Generate this.

Don't change that.

Follow this structure.

Only modify these files.

Run these tests.

But as the development tasks became more complicated, the prompts became longer.

Every new failure produced another instruction.

Every unexpected modification produced another restriction.

Every architectural misunderstanding produced another explanation.

Eventually, starting a task meant carrying a growing list of instructions into the conversation.

The prompt was no longer just describing what I wanted the AI to do.

It was also carrying everything I did **not** want the AI to do.

That was probably my first informal rule system.

I just didn't call it one yet.

[[L_BRA_A_01-1.png]]

---

## Then I Put the Rules Closer to the Code

The next idea seemed obvious.

If a particular piece of code should not be modified, why keep telling the AI about it in every prompt?

Put the instruction where the code is.

So I started using comments to mark things such as:

> This section can be modified.

or:

> Do not change this implementation.

This improved locality.

The rule was closer to the thing it governed.

But it introduced another problem.

These instructions were now mixed with the source code itself.

They could accidentally become part of a commit.

They could remain after the AI task was finished.

And temporary AI-development instructions were beginning to contaminate production artifacts.

I had moved the rule closer to its scope.

But I had also mixed two different concerns:

**software implementation** and **AI behavioral control**.

---

## Project Instructions Were Better

Project-level instruction files were a much cleaner solution.

For example, a `CLAUDE.md` file could describe how an AI coding assistant should behave within a repository.

Now I didn't have to repeat the same instructions in every prompt.

The instructions could persist with the project.

That was a major improvement.

But another limitation gradually became visible.

Many of the rules I was writing weren't really unique to one project.

"Don't modify artifacts outside the declared scope."

"Don't silently change interfaces."

"Don't create undeclared artifacts."

"Preserve traceability."

"Don't modify tests simply to make an implementation pass."

These were not necessarily properties of one repository.

They were recurring **development behavior rules**.

Copying them from project to project worked.

But copying wasn't the same thing as managing them.

---

## So I Started Building a Rule List

That changed the way I looked at these instructions.

Instead of asking:

> What instructions does this project need?

I started asking:

> Which rules keep appearing across projects and development situations?

I extracted them.

Named them.

Grouped them.

Removed duplicated wording.

Separated project-specific instructions from reusable behavioral constraints.

What had previously been embedded in prompts, comments, and project files gradually became a **rule list**.

That was an important transition.

A rule was no longer something I happened to write inside a prompt.

It started becoming something that could exist independently.

---

## Then Individual Rules Were Not Enough

A development task rarely needs every rule.

A coding task may need one set.

A testing task may need another.

A structural refactoring task may require additional constraints.

A high-risk change may require stricter rules than a routine modification.

So the next step was to package rules according to context.

Individual rules became reusable building blocks.

Selected combinations became **rulesets**.

Conceptually:

```text
Rule A ─┐
Rule B ─┼──> Ruleset: Coding
Rule C ─┘

Rule B ─┐
Rule D ─┼──> Ruleset: Refactoring
Rule E ─┘

Rule A ─┐
Rule E ─┼──> Ruleset: High-Risk Change
Rule F ─┘
```

Instead of maintaining one enormous instruction block, I could select a ruleset for a particular development situation.

---

## The Rules Became Documents

At this point, another change happened.

The rules were no longer merely part of the conversation.

They became documents.

A task could load the appropriate ruleset directly into the prompt or development workflow.

The pattern had changed from:

```text
Remember all these instructions
            ↓
          Prompt
            ↓
            AI
```

to:

```text
Rule Library
     ↓
Select Ruleset
     ↓
Development Context
     ↓
Prompt / AI Workflow
```

This solved a practical problem I had been dealing with since the beginning:

I no longer needed to manually reconstruct the same behavioral instructions every time I started a new task.

But it also created a much more interesting problem.

[[L_BRA_A_01-2.png]]

---

## At What Point Does a List of Rules Become an Architecture?

Once rules became reusable documents, questions started appearing that a simple rule list could not answer.

What exactly is a rule?

How should a rule be identified?

Should a rule contain one behavioral constraint or several?

Who owns it?

Where does it apply?

Can two rules contradict each other?

Can a ruleset change the meaning of a rule?

How should rules be categorized?

How should they be versioned?

What happens when the same rule is used by different projects, agents, or models?

And eventually:

> **If rules are becoming reusable engineering artifacts, should they still be treated merely as text loaded into a prompt?**

That was the point where my problem changed.

I was no longer trying to write better prompts.

I was trying to understand the architecture behind the rules themselves.

That eventually became **Behavior Rule Architecture (BRA)**.

But BRA did not begin as an architecture.

It began with a much more ordinary problem:

**I was tired of carrying the same long list of instructions into every AI development session.**

Prompt by prompt.

Comment by comment.

Project by project.

Rule by rule.

Eventually, the instructions became something else.

And that raises the question I want to start this series with:

> **When did your AI instructions start becoming rules?**

#BehaviorRuleArchitecture #AIEngineering #PromptEngineering #SoftwareEngineering
