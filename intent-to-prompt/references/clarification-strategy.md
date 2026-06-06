# Clarification Strategy

Ask the fewest questions needed to make the final prompt materially better. The user is trying to move work forward, not fill out a form.

## Question Budget

- Default: 0-3 questions.
- Ask 1 question when one missing decision dominates the task.
- Ask 2-3 questions when multiple missing details would change the prompt.
- Ask more only if the user explicitly wants a rigorous intake process.

## Ask vs Assume

Ask when:

- the answer changes the task scope, deliverable, or success criteria
- the task can cause destructive, expensive, external, or risky actions
- the target audience, data source, or editable files are unclear
- the user wants a high-quality reusable prompt

Assume when:

- the assumption is conventional and low-risk
- the user asks for speed or "just draft it"
- the task is exploratory
- the final prompt can tell the agent to confirm details before acting

When assuming, include an `Assumptions` section before the final prompt.

## High-Value Questions by Missing Dimension

**Objective**

- "What exact deliverable should the agent produce?"
- "What outcome matters most: speed, completeness, correctness, creativity, or minimal changes?"

**Context**

- "Who is the intended audience or user of the final output?"
- "What background should the agent know that is not obvious from the task?"

**Inputs**

- "What source materials should the agent use as ground truth?"
- "Are there files, links, examples, or screenshots the agent must inspect?"

**Scope**

- "What is explicitly out of scope?"
- "For a coding task, which files or modules can the agent change?"

**Workflow**

- "Should the agent first propose a plan for approval, or proceed directly?"
- "Should the agent research first, inspect existing work first, or start from your description?"

**Output**

- "What final format do you want: code patch, markdown brief, table, JSON, checklist, or something else?"
- "Should the final answer be concise, detailed, or copy-ready for publication?"

**Validation**

- "How should the agent prove the task is complete?"
- "Are there tests, metrics, citations, screenshots, or acceptance criteria it should use?"

**Permissions and risk**

- "Can the agent edit files, run commands, browse the web, or call external services?"
- "What actions should require confirmation before proceeding?"

## Clarifying Question Output

Use this format:

```markdown
## Clarifying Questions

1. ...
2. ...
3. ...
```

If useful, add one sentence:

```markdown
After these, I can generate a copy-ready agent prompt.
```

Do not provide a final prompt in the same response unless the user asks for a draft with assumptions.

## Handling User Answers

When the user answers:

1. Integrate their answers into the final prompt.
2. Do not ask another round unless a new critical ambiguity appears.
3. If answers remain partial, proceed with labeled assumptions.
