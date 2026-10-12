# Same Prompt. Different Context. Which AI Change Can You Defend?

**Engineering Before Governance — Main Series 04 / 08**

[[X_EBG_A_04-0.png]]

“We saved the prompt, so we can explain the change.”

“We saved the code, so we can review the result.”

Both records help. Neither establishes which specification, rules, source fragments, permissions, and conversation state the agent actually received.

Two runs can share the same visible request while operating under different engineering conditions. That difference matters when someone must defend the result.

## The code can survive while its basis disappears

An engineer asks an agent to add one retry for temporary payment failures, preserve idempotency, keep the public API unchanged, and run integration tests.

The agent edits the code. Two weeks later, the pull request and prompt remain.

But the team cannot resolve which payment specification was delivered, whether the architecture constraint entered context, or whether a conversation summary dropped a requirement.

Git preserves repository state. A specification preserves intent. Conversation history preserves visible interaction. Logs and test results retain selected events.

The missing connection is which versions and conditions came together in this particular run.

## Available is not delivered

A document in the repository was **available**. A tool log may show it was **accessed**. A context assembly record can show what was **delivered**. A final summary may **claim** that it influenced the result.

These are separate claims with different evidence.

A read event does not necessarily establish that complete content reached a later model request. Retrieval may select fragments. Tools may truncate output. Summaries may transform earlier material.

The record should identify only the state that can be established. If a platform does not expose part of context assembly, preserve that limit as unknown.

## Preserve three views of the run

**What the run should receive.** Preserve a versioned Prompt Artifact, approved Change Scope, and references to required system views and rules.

**What the run actually received.** A Context Manifest identifies delivered instructions, specification fragments, source states, tool capabilities, permissions, and relevant environment conditions. Capture retrieval, summarization, omission, or truncation when observable.

**What connects the basis to the result.** A Development Change ID links the prompt, manifest, decisions, tool actions, artifacts, and verification. Individual decisions retain their identities within the run.

Those references must resolve to historical state. A manifest pointing only to mutable “latest” documents cannot preserve the basis of an earlier run.

## Compare expected and observed conditions

Suppose the payment retry change requires three viewpoints: business rules for temporary failures, system design for retry limits, and architecture constraints on a shared transaction boundary.

The manifest supports delivery of the first two. Architecture delivery was not captured. The diff also modifies the shared boundary outside approved scope.

These are separate findings:

- required architecture delivery is unproven;
- an artifact outside the authorized boundary was modified.

Unproven delivery does not establish that the model knew nothing about the architecture. It establishes that the required delivery claim cannot be supported. The out-of-scope modification has its own observable basis.

An authorized maintainer can return the change, restore the boundary, supply the missing viewpoint, and request a new generation under a corrected basis.

## Aim for basis reproducibility

Retaining controlled inputs does not guarantee that another run will produce identical code. A more useful goal is **basis reproducibility**: another reviewer can recover the versioned inputs and conditions against which the work should be judged.

Sensitive content can stay in controlled storage. The manifest may carry identifiers, versions, integrity hashes, and access classifications, as long as authorized reviewers can resolve what they need.

For your next AI-assisted change, record the approved basis before generation and the observed basis during execution. Review the difference alongside the code diff and tests.

Which constraint in your current workflow is assumed to reach the model but is not actually captured as delivered?

## Sources

- [W3C PROV-O](https://www.w3.org/TR/prov-o/)
- [Viewpoint-Structured Specification](https://doi.org/10.31224/6612)
- [Ghost Intent](https://doi.org/10.5281/zenodo.18872540)

#EngineeringBeforeGovernance #ContextEngineering #AIGovernance #AIEngineering
