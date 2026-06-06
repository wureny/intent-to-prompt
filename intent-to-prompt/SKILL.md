---
name: intent-to-prompt
description: Convert rough user intent into precise, complete, agent-ready prompts. Use when the user wants help writing, improving, compiling, or debugging prompts for AI agents or LLM tools; when they say things like "write a prompt for Codex/Claude/Gemini/ChatGPT", "turn this intent into a better prompt", "help me ask an agent to do this", "optimize this prompt", "make this task clearer for an agent", or when a vague task would benefit from clarification before being handed to a coding, research, writing, data, design, automation, image, or general-purpose agent. Works in Chinese and English.
---

# Intent to Prompt

Convert a user's rough intent into an execution-ready prompt for an AI agent. Optimize for task completion quality, not prompt cleverness.

The output is usually either:
- a small set of clarification questions before writing the final prompt, or
- a final prompt the user can paste into an agent.

## Core Principle

Treat prompt engineering as specification engineering. A strong agent prompt defines the objective, context, inputs, scope, workflow, output contract, quality bar, and validation path.

Do not merely polish wording. Diagnose what the agent would need to know to complete the task correctly.

## Workflow

### 1. Classify the Task

Identify the primary task type:

- **coding**: build, debug, refactor, test, review, ship, inspect a repo
- **research**: web/source-backed research, comparison, synthesis, due diligence
- **writing**: article, memo, email, PRD, strategy doc, speech, narrative
- **data-analysis**: spreadsheet, SQL, dashboard, metric diagnosis, charting
- **design**: product design, prototype, UI/UX, visual QA, flow design
- **image-video**: image generation/editing, visual prompt, video prompt
- **automation-agent**: multi-step agent workflow with tools, permissions, stopping rules
- **general**: anything else

For detailed task-specific modules, read `references/task-modules.md` only for the relevant task type.

### 2. Select the Output Mode

Choose the lightest mode that satisfies the user's situation:

- **Quick Prompt**: for simple one-off tasks. Produce a compact prompt with objective, context, constraints, deliverable, and validation.
- **Agent Prompt**: for coding, research, data, design, and automation agents. Produce a structured prompt with workflow, scope, quality bar, and validation.
- **Product Prompt**: for prompts embedded in apps, reusable workflows, teams, or open-source examples. Include variables, label definitions, examples, output schema, failure handling, and evaluation checks.

Default to Agent Prompt when the user mentions Codex, Claude Code, Gemini CLI, an "agent", repository work, tool use, or multi-step execution.

### 3. Audit Prompt Readiness

Score the user's intent silently against the rubric in `references/prompt-quality-rubric.md`.

Look for missing or weak:

- objective
- context and audience
- inputs and source materials
- scope and non-goals
- constraints and preferences
- workflow expectations
- output format
- quality bar
- validation or success criteria
- risk, permission, or uncertainty handling

Do not show a long rubric report unless the user asks. Use the audit to decide whether to ask questions or produce a prompt.

### 4. Decide Whether to Ask Clarifying Questions

Ask questions only when an answer would materially change the final prompt.

Use this decision rule:

- **Proceed directly** when the objective, context, scope, output, and success criteria are clear enough.
- **Ask 1-3 questions** when key missing information would change what the agent should do.
- **Use assumptions** when the user asks for speed, when missing details are low-risk, or when reasonable defaults are obvious.
- **Refuse to over-specify** when the user's task is exploratory and would benefit from agent discovery.

For question selection patterns, read `references/clarification-strategy.md`.

When asking questions, stop after the questions. Do not also provide a final prompt unless the user explicitly requested a draft under assumptions.

### 5. Build the Draft Prompt

Use the template in `references/templates.md`. Include only sections that help execution.

A strong default structure:

```markdown
# Objective

# Context

# Inputs

# Scope

# Workflow

# Output Requirements

# Quality Bar

# Validation
```

Adapt the user's language. If the user writes in Chinese, produce Chinese surrounding text and usually a Chinese prompt unless they ask otherwise. Preserve domain terms and proper nouns.

### 6. Adapt to the Target Agent

If the user names a target agent or tool, adapt the prompt to that agent's real capabilities. If they do not name one, keep the prompt agent-neutral.

Read `references/target-agent-adaptation.md` when the target agent matters, especially for Codex, Claude Code, Gemini CLI, ChatGPT, research agents, image/video models, or product-embedded prompts.

### 7. Add Execution Aids When Useful

Use advanced prompting strategies only when they improve likely task completion:

- **Few-shot examples**: add when format, tone, classification, extraction, or style consistency matters.
- **Task decomposition**: add when the task is complex, multi-stage, or failure-prone.
- **Reference grounding**: add when factual accuracy, source fidelity, or repo/file context matters.
- **Structured output**: add when the result must be parsed, compared, reviewed, or reused.
- **Self-check / validation loop**: add when mistakes are costly or the task has testable acceptance criteria.
- **Tool and permission rules**: add when the target agent can browse, edit files, run commands, call APIs, or affect external systems.
- **Assumption management**: add when proceeding without clarification.
- **Stop conditions**: add when the agent should pause before destructive, expensive, irreversible, or ambiguous actions.

Read `references/examples-and-few-shot-strategy.md` when the task depends on style imitation, label boundaries, extraction consistency, structured output, product-embedded prompts, or repeated workflow reliability.

Avoid asking for hidden chain-of-thought. Prefer instructions such as "work step by step internally, then provide the concise result and validation notes."

### 8. Review and Revise Once

Before returning the final prompt, internally review the draft and revise it once.

Check:

- Is the definition of done unambiguous?
- Are context, inputs, and instructions clearly separated?
- Is there a validation path where correctness can be checked?
- Are assumptions explicit rather than hidden?
- Does the prompt avoid common anti-patterns?
- Is any section decorative, redundant, or too broad?
- Is the prompt adapted to the target agent without hard-coding irrelevant tool behavior?

Read `references/prompt-anti-patterns.md` when the draft feels verbose, generic, brittle, or likely to produce shallow agent output.

Only make revisions that improve execution quality. Do not expand the prompt just to look thorough.

### 9. Return the Result

Default output formats:

If clarification is needed:

```markdown
## Clarifying Questions

1. ...
2. ...
3. ...
```

If ready:

```markdown
## Final Agent Prompt

[copy-ready prompt]

## Why This Works

- [1-3 concise bullets explaining the main prompt-engineering upgrades]
```

If using assumptions:

```markdown
## Assumptions

- ...

## Final Agent Prompt

[copy-ready prompt]
```

Keep explanation secondary. The prompt is the product.

## Quality Checks Before Responding

Before finalizing, verify:

- The prompt can be pasted into an agent without needing this conversation.
- The objective is concrete enough for the agent to know when it is done.
- Inputs and context are distinguishable from instructions.
- Scope includes non-goals or boundaries when overreach is likely.
- Output requirements specify format, language, and level of detail where needed.
- Validation exists for tasks where correctness can be checked.
- The prompt does not invent constraints the user did not imply unless clearly labeled as assumptions.
- The prompt is no longer than the task needs.

## Reference Map

- `references/prompt-quality-rubric.md`: readiness rubric and diagnosis signals.
- `references/clarification-strategy.md`: when and what to ask before writing the prompt.
- `references/task-modules.md`: task-specific prompt modules.
- `references/target-agent-adaptation.md`: adapt prompts to specific agent/tool capabilities.
- `references/prompt-anti-patterns.md`: detect and fix common prompt failures.
- `references/examples-and-few-shot-strategy.md`: decide when and how to use examples.
- `references/templates.md`: reusable prompt templates.
- `references/examples.md`: realistic examples of raw intent, questions, and final prompts.
