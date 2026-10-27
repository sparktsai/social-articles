I wasn't trying to build AI governance.

In 2025, I was using Copilot agents and the Claude Code CLI to generate code. My problem was correctness.

A change would contain a bug. I would ask AI to fix it. The next revision might introduce another problem, while the diff rewrote almost everything.

I asked AI how to make specification and code generation more stable without waiting for a better model.

Its answer was: this requires governance.

That was not what I expected. I wanted reliable changes, not a governance system.

So I asked why.

The explanation began with the probabilistic nature of GenAI. If I wanted to understand why AI changed the code, whether it used the intended basis, and where it diverged, the final output was not enough.

The answer drew from the Digital Omnibus discussion and ISO/IEC 42001. It reminded me of working with BS 7799 more than twenty years earlier.

There were policies, requirements, and audits. But the same question remained: how do people make them work in practice?

I saw a similar gap in AI governance.

Most discussions focused on data governance or AI making decisions for people at runtime. There was much less to reuse for decisions made while software was being developed.

So I started from engineering.

I tried to make AI decision evidence visible, adjust scope and boundaries, establish rules, and trace how specifications influenced code and AI decisions.

None of this began as governance theory. It began as an attempt to understand unstable development behavior.

But visibility alone was not enough. What became visible had to become usable engineering. And those mechanisms had to keep improving through a simple cycle: define, observe, compare, and adjust.

That was when engineering and governance stopped looking like opposite ends of the problem.

Engineering makes decisions observable and controllable.

Governance gives those mechanisms purpose, responsibility, and a reason to improve.

They are two sides of the same work.

For me, that realization began with a bad diff—not an elaborate theory.

And the boundary of this work remains deliberate: AI governance during software development.
