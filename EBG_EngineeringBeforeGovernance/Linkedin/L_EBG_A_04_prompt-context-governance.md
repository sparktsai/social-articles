# Same Prompt. Different Context. Which AI Change Can You Defend?

**Engineering Before Governance | 04 / 08**

"We saved the prompt, so we can explain the change."

"We saved the code, so we can review the result."

Both records help. Neither establishes which specification, rules, source fragments, permissions, and conversation state the agent actually received.

Two runs can share the same visible request while working from different engineering conditions. That difference matters when a reviewer must judge the resulting change.

[[L_EBG_A_04-0.png]]

## The development basis can disappear while the code survives

An engineer asks an agent to add one retry for temporary payment failures, preserve idempotency, keep the public API unchanged, and run integration tests.

The agent edits the code. Two weeks later, the pull request and prompt remain available.

But the team cannot resolve which payment specification version was delivered, whether the architecture constraint entered context, or whether a conversation summary dropped a requirement.

Git can recover repository state. A persistent specification can preserve intent. Conversation history can preserve visible interaction. Telemetry and test results retain selected events and checks.

The missing connection is which versions and conditions came together in this particular run.

## Distinguish available information from delivered information

[[L_EBG_A_04-1.png]]

A document in the repository was **available**. A tool log may show that a file was **accessed**. A context assembly record can show what was **delivered**. A final summary may **claim** that a constraint influenced the result.

Those are separate claims with different evidence.

A read event alone does not establish whether the complete content reached a later model request. Retrieval may select fragments; tools may truncate output; summaries may transform prior material.

The manifest should identify the state that can actually be established. If the platform does not expose part of context assembly, retain that limit as unknown.

## Preserve three things around each run

**What the run should receive.** Preserve a versioned Prompt Artifact, the approved Change Scope, and references to the required system views and rules.

In this series, **Viewpoint-Structured Specification (VSS)** represents system knowledge through relevant viewpoints such as business analysis, system design, and architecture. Scope selects the bounded modification and its exclusions.

[[L_EBG_A_04-2.png]]

**What the run actually received.** A Context Manifest identifies delivered instructions, specification fragments, source states, tool capabilities, permissions, and relevant environment conditions. Capture summarization, retrieval, omission, or truncation when observable.

**What connects the basis to the result.** A Development Change ID links the prompt, manifest, decisions, tool actions, artifacts, and verification. Individual decisions retain their own identities within the run.

The references must resolve to historical state. A manifest pointing only to mutable "latest" documents cannot preserve the basis of an earlier run.

## Compare the expected and observed basis

Suppose the approved payment retry change requires three viewpoints: business rules for temporary failures, system design for retry limits, and architecture constraints on the shared transaction boundary.

The observed manifest supports delivery of the first two. Architecture delivery was not captured. The diff also contains a modification to the shared transaction boundary outside approved Scope.

These are two distinct findings:

- required architecture delivery is unproven;
- an artifact outside the authorized boundary was modified.

Unproven delivery does not establish that the model lacked all architecture knowledge. It establishes that the required delivery claim cannot be supported. The out-of-scope diff has its own observable basis.

The authorized maintainer can use these findings to return the change, restore the boundary, supply the required viewpoint, and request a new generation under a corrected basis.

[[L_EBG_A_04-3.png]]

## Recover the basis without promising identical output

Retaining controlled inputs and conditions does not guarantee that another model run produces identical code. The more useful goal is **basis reproducibility**: another reviewer can recover the versioned inputs and conditions against which the work should be judged.

Sensitive content can remain in controlled storage. The manifest can carry identifiers, versions, integrity hashes, and access classifications, provided authorized reviewers can resolve the necessary material.

For your next AI-assisted change, record the approved basis before generation and capture the observed basis during execution. Review the differences alongside the diff and tests.

This makes a missing constraint or unexpected permission a finding that someone can act on, rather than a detail the team hopes to remember later.

## Further Reading

- [W3C PROV-O](https://www.w3.org/TR/prov-o/)
- [Spark Tsai: Viewpoint-Structured Specification](https://doi.org/10.31224/6612)
- [Spark Tsai: Ghost Intent](https://doi.org/10.5281/zenodo.18872540)
