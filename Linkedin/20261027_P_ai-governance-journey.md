# I Wasn't Trying to Build AI Governance

I encountered AI governance in 2025, but it was not what I was looking for.

I was using Copilot agents and the Claude Code CLI to generate code. My problem was simpler: correctness.

A change would contain a bug. I would ask AI to fix it. The next revision might introduce another problem, while the diff rewrote almost everything.

I began asking AI how to make generated specifications and code more stable without simply waiting for a better model.

By Q4 2025, my concern was practical: how could each prompt continue from what was already established instead of starting over?

AI's answer was that this required governance.

That was not the answer I expected. I was not trying to build governance. I only wanted more reliable changes.

So I asked why.

The explanation began with GenAI's probabilistic nature. To understand why AI changed the code, whether it used the intended basis, and where it diverged, the final output was not enough.

The answer also drew from the Digital Omnibus discussion and ISO/IEC 42001. It reminded me of introducing information security under BS 7799 more than twenty years earlier.

There were policies, requirements, and audits. But a question always remained: how should people make them work in practice?

I saw a similar gap in AI governance. Most discussions focused on data or AI making decisions for people at runtime. There was little to reuse for decisions made during software development.

And if GenAI development itself was still unstable, what exactly could governance govern?

I decided to begin from the engineering side.

I tried to make AI decision evidence visible, adjust scope and boundaries to reduce divergence, establish the rules AI had to follow, and trace how specifications influenced code and AI decisions.

None of these began as governance theory. They began as attempts to understand and correct unstable development behavior.

But as the work continued, something became clearer.

Visibility alone was not enough. What became visible had to be turned into engineering mechanisms that people could actually use.

And those mechanisms could not remain static. Throughout the research, I kept returning to the same cycle: define what should happen, observe what actually happened, compare it with the evidence, and improve the boundary, rule, context, or control.

That was when engineering and governance stopped looking like opposite ends of the problem.

Engineering makes decisions observable and controllable. Governance gives those mechanisms purpose, responsibility, and a reason to improve.

They are two sides of the same work—and reaching that conclusion did not require an elaborate theory. It began with a bad diff and a practical question about correctness.

The boundary of this work is deliberate: AI governance during software development.

#AIGovernance #AISoftwareDevelopment #SoftwareEngineering
