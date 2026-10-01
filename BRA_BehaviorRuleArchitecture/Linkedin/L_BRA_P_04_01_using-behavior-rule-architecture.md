# LBRA-04 — How Do You Actually Use a Behavior Rule Architecture?

## Problem

An architecture is useful only if it can be applied inside real development work.
The practical question is how to give the AI the right Rules for the current task without copying heavy governance artifacts into every prompt.

## Outline

This post follows the usage model from prompt-selected Rulesets to a Rule Library.
It explains why complete Rule artifacts are useful for governance but too heavy for routine inference.
It then shows how Skills and CLI-style consumers can resolve compact execution views from the authoritative Rule Library.

## Brief

Early BRA usage was simple: select the relevant Ruleset for the development scenario and include it in the prompt.
That worked better than one universal prompt, but complete Rules contained governance information that the LLM did not need for every task.
The solution was to preserve complete Rules in the Rule Library while giving the model a smaller execution view, typically ID, version, and CNL.
At first, that compact view could be stored separately, but that created a synchronization problem between the authoritative Rule and the execution copy.
Skills changed the model by resolving the latest relevant Rules when the task starts, instead of maintaining another source of truth.
CLI operations can expose the same infrastructure for humans, scripts, validation, inspection, and other development tooling.

## Conclusion

BRA is not a prompt, a Skill, or a CLI.
BRA defines the Rule architecture, while the Rule Library provides the infrastructure that different consumers can use without redefining the Rules.
