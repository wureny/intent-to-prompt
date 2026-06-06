# Examples and Few-Shot Strategy

Use this when examples could materially improve the prompt. Examples are one of the highest-leverage prompt components, but only when they clarify behavior the model cannot infer reliably from description alone.

## Contents

- [When Examples Are High Value](#when-examples-are-high-value)
- [When Not to Use Examples](#when-not-to-use-examples)
- [Clarifying Questions for Examples](#clarifying-questions-for-examples)
- [Example Set Design](#example-set-design)
- [Synthetic Examples](#synthetic-examples)
- [Product-Embedded Prompt Pattern](#product-embedded-prompt-pattern)
- [Example Quality Checklist](#example-quality-checklist)

## When Examples Are High Value

Prefer examples when the task depends on:

- **style or voice**: emails, essays, brand copy, executive memos, social posts
- **classification boundaries**: support tickets, risk labels, lead quality, moderation categories
- **information extraction**: contracts, emails, receipts, resumes, web pages, logs
- **structured outputs**: JSON, tables, schemas, API-ready payloads
- **judgment calibration**: priority, severity, confidence, escalation, pass/fail
- **design taste**: dense dashboard vs marketing page, enterprise UI vs playful app
- **code conventions**: error handling, test style, API wrapper style, naming patterns
- **repeated workflow prompts**: prompts embedded in products or team processes

If one of these applies and no examples are provided, consider asking for examples before writing the final prompt.

## When Not to Use Examples

Do not add examples when:

- the task is a simple one-off instruction
- examples would make the prompt longer without reducing ambiguity
- the user needs speed and the missing examples are low-risk
- examples could leak private or sensitive data
- the task requires current facts or source grounding more than behavior calibration
- the target agent should discover patterns from the repository, dataset, or documents directly

For coding agents, prefer "inspect nearby files/tests and follow local patterns" over invented examples unless the user wants a reusable coding prompt.

## Clarifying Questions for Examples

Ask at most 1-2 example-related questions.

High-value questions:

1. "Do you have 1-3 examples of ideal outputs, or examples of outputs you dislike?"
2. "For classification/extraction, what are the allowed labels or schema fields?"
3. "Are there borderline cases where the model often gets the decision wrong?"
4. "Should I generate illustrative examples if you do not have real ones?"

Ask for examples before the final prompt when:

- examples define label boundaries
- the prompt will be reused in production
- style/voice matters more than generic quality
- the user has complained that previous outputs were inconsistent

Proceed with synthetic examples when:

- the user asks for a draft
- the examples are only meant to demonstrate structure
- the final prompt clearly labels them as illustrative

## Example Set Design

A strong few-shot set usually includes:

- **positive examples**: what good output looks like
- **negative examples**: what to avoid, when useful
- **borderline examples**: hard cases that define boundaries
- **counterexamples**: cases that look similar but should produce different outputs

Keep example count small:

- 1-2 examples for style
- 3-5 examples for classification or extraction
- 2-3 examples for structured output
- more only when the user is building a production prompt and examples are compact

For each example, make clear what the example teaches:

```markdown
## Examples

These examples define tone, structure, and decision boundaries. Do not copy their facts.

### Example 1: [what this demonstrates]
Input:
...

Output:
...
```

## Synthetic Examples

Synthetic examples can help when the user has no real examples, but they must not pretend to be real data.

Rules:

- Label them as `Illustrative examples`.
- Keep them generic and privacy-safe.
- Do not invent domain facts that the final agent should rely on.
- Use them to demonstrate format, tone, schema, or decision rules.
- Tell the target agent not to treat synthetic examples as source material.

Useful clause:

> The examples below are illustrative only. Use them to learn the desired format and decision rules, not as factual source material.

## Product-Embedded Prompt Pattern

For prompts that will run inside an app, examples should be tied to schema and evaluation.

Include:

- input variables
- allowed labels or field definitions
- output JSON schema
- examples for common and borderline cases
- tie-break rules
- fallback behavior
- evaluation checks

Pattern:

~~~markdown
# Inputs

- `ticket_subject`: ...
- `ticket_body`: ...

# Labels

- `billing`: ...
- `bug`: ...
- `feature_request`: ...
- `account_access`: ...

# Tie-Break Rules

- If the ticket mentions a payment failure caused by an error message, classify as `billing` unless the user cannot log in.
- If two labels apply, choose the label that determines the first routing action.

# Output Format

Return JSON only:
```json
{
  "label": "billing | bug | feature_request | account_access",
  "confidence": 0.0,
  "rationale": "one short sentence",
  "needs_human_review": true
}
```

# Illustrative Examples

[3-5 compact examples]
~~~

## Example Quality Checklist

Before including examples, verify:

- The examples are shorter than the instructions they replace or materially clearer.
- They cover real ambiguity, not obvious cases only.
- They do not introduce accidental constraints.
- They do not conflict with written rules.
- They are labeled as real or illustrative.
- They avoid sensitive data unless the user intentionally provided it for this task.
- The prompt says which parts of the examples to imitate: format, tone, labels, schema, or reasoning standard.
