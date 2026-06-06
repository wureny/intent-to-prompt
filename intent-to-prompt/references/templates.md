# Templates

Use these as starting points. Remove sections that do not help the task.

## Contents

- [Universal Agent Prompt](#universal-agent-prompt)
- [Compact Prompt](#compact-prompt)
- [Coding Agent Prompt](#coding-agent-prompt)
- [Research Prompt](#research-prompt)
- [Reusable Product Prompt](#reusable-product-prompt)

## Universal Agent Prompt

```markdown
# Objective

[State the concrete outcome the agent should achieve.]

# Context

[Give the background the agent needs to make good decisions.]

# Inputs

[List files, links, pasted text, screenshots, data, examples, or other source material.]

# Scope

Do:
- [Required work]

Do not:
- [Non-goals, boundaries, forbidden changes]

# Workflow

1. [First action: inspect, research, ask, plan, or proceed.]
2. [Main execution step.]
3. [Review/refine step.]
4. [Validate the result.]

# Output Requirements

[Specify final format, language, level of detail, structure, and any machine-readable schema.]

# Quality Bar

[Define what good means for this task.]

# Validation

[Specify tests, checks, citations, screenshots, examples, acceptance criteria, or review process.]

# Assumptions and Uncertainty

[Tell the agent how to handle missing information, uncertainty, and when to ask follow-up questions.]
```

## Compact Prompt

```markdown
Please complete this task: [objective].

Context: [context].

Use these inputs as ground truth: [inputs].

Constraints: [scope, non-goals, preferences].

Deliverable: [output format].

Before finishing, validate by [checks].

If a key detail is missing, make a reasonable assumption and state it; ask before taking risky or irreversible actions.
```

## Coding Agent Prompt

```markdown
# Objective

[Implement/fix/refactor/build/review X.]

# Context

[Repo/product/background context.]

# Scope

- In scope: [files, modules, behavior, screens, tests]
- Out of scope: [unrelated refactors, redesigns, dependencies, API changes]

# Workflow

1. Inspect the relevant code and existing patterns before editing.
2. Briefly identify the implementation approach.
3. Make the smallest coherent change that satisfies the objective.
4. Add or update focused tests when the behavior is testable.
5. Run relevant validation commands. If a command cannot run, explain why and provide the best alternative check.

# Constraints

- Preserve existing behavior outside the requested change.
- Do not revert unrelated user changes.
- Follow the repository's existing style and abstractions.
- Ask before destructive, irreversible, or broad changes.

# Output Requirements

Return a concise summary of:
- what changed
- files touched
- validation run and results
- remaining risks or follow-ups
```

## Research Prompt

```markdown
# Research Objective

[Question to answer and decision this research supports.]

# Scope

- Geography/time period: [scope]
- Include: [topics/sources]
- Exclude: [non-goals]

# Source Requirements

- Prefer primary or official sources where available.
- Use recent sources for facts that may have changed.
- Cite sources with links.
- Distinguish sourced facts from inference.

# Workflow

1. Gather sources.
2. Cross-check important claims.
3. Synthesize findings around the decision question.
4. Flag uncertainty, disagreements, and weak evidence.

# Output

[Brief/table/memo/recommendation format.]
```

## Reusable Product Prompt

Use when the user is designing a prompt to embed in an app or workflow.

~~~markdown
# Role

[What the model should act as, only if role affects behavior or tone.]

# Task

[What the model must do for each invocation.]

# Inputs

The model will receive:
- `[variable_name]`: [meaning]
- `[variable_name]`: [meaning]

# Instructions

- [Core instruction]
- [Decision rule]
- [Constraint]
- [Safety or uncertainty rule]

# Output Format

Return:
```json
{
  "field": "description"
}
```

# Examples

## Example 1
Input:
[example input]

Output:
[ideal output]

# Quality Checks

Before responding, verify:
- [check]
- [check]
~~~
