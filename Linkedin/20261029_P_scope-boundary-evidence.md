# The Same Prompt Did Not Produce the Same Change

My path into AI governance began with a bad diff. The next step began with a simple observation: the same prompt did not lead AI to change the same things.

I was asking AI to modify a specification or a piece of code. The difference between the first and second result was not just wording or naming style.

The scope of the change was different.

So I repeated the same prompt ten times. Then I tried it with different models.

The results left me with a mental picture.

Imagine a sentence as a beam of light passing through many layers of filters. Each layer contains openings of different sizes and directions. The signal follows one probable path through them and eventually forms the answer we see.

Send the same sentence again, and the path may be similar—but not identical.

That picture did not explain the model. But it changed how I approached the problem.

Instead of asking only what I wanted AI to do, I first wrote down what I expected it to change. Then I compared that expectation with what it actually changed.

I began putting that expectation into the prompt, together with limits on what should remain untouched.

The results became noticeably more contained.

This was how Scope and Boundary became practical for me.

**Scope described the intended area of change. Boundary described where the change should stop.**

Then I encountered another problem.

After AI completed a change, I asked why it had made that decision. The answer was not convincing, so I asked the same question five times.

Each explanation was different.

I changed the timing. Instead of asking for reasons afterward, I asked AI to provide them while making the change:

- Why this choice?
- What alternatives were considered?
- Why were they not selected?

The answers were not identical every time, and they were not proof of a model's hidden internal reasoning. But they became stable enough to compare the decision with the resulting change.

That was how Evidence became practical for me—not as a story reconstructed after the work, but as a record produced alongside it.

Looking back, none of this began as a theory about governance.

It began with three ordinary questions:

**What did I intend AI to change?**

**Where should it stop?**

**What record would let me understand and review the decision?**

Those questions eventually led to a Scope paper, an Evidence skill, a way to visualize AI inference, and testable development flows across models and technology stacks.

More importantly, they changed how I understood governance during software development.

Governance did not arrive as another layer placed above engineering. It emerged from making engineering intent, limits, and decisions visible enough to examine and improve.

#AIGovernance #AISoftwareDevelopment #SoftwareEngineering
