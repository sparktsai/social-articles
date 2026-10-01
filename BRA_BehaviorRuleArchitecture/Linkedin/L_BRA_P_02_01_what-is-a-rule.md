# LBRA-02 — What Is a Rule?

## Problem

Moving instructions out of prompts does not automatically make them clear Rules.
If natural-language instructions still require the AI to infer obligation, prohibition, action, target, and applicability, then reuse only moves ambiguity into another file.

## Outline

This post examines why a Rule needs more than a useful sentence.
It follows the progression from natural language to NNL, CNL, MUST and MUST NOT, Policy and Constraint, Action and Target, and Applicability.
It then explains why a Rule should separate required or prohibited behavior from the context where that behavior applies.

## Brief

The article begins with a deceptively simple question: what exactly is a Rule?
Many statements can look like rules, including preferences, recommendations, coding guidelines, restrictions, or project instructions.
To make behavior more stable, sentence structure first had to become clearer through Normative Natural Language, and normative vocabulary then had to become narrower through Constraint Normative Language.
Eventually, MUST and MUST NOT became the most useful expressions because they expose whether behavior is required or prohibited.
But polarity alone was not enough; a Rule also had to identify the governed action and target, such as modifying test code while fixing source code.
That exposed another design boundary: the Rule should express the behavioral constraint, while applicability should describe where and when that constraint applies.

## Conclusion

A reusable Rule is not just an instruction that can be copied.
It is a structured behavioral statement that makes intent explicit enough to remain stable across changing development contexts.
