# Prompt Anti-Patterns

Use this during the internal review step. The goal is not to make the prompt longer; it is to remove failure modes that cause weak agent execution.

## Contents

- [Role Decoration Without Operational Value](#role-decoration-without-operational-value)
- [Vague Quality Words](#vague-quality-words)
- [No Output Contract](#no-output-contract)
- [Hidden Assumptions](#hidden-assumptions)
- [Context and Instructions Mixed Together](#context-and-instructions-mixed-together)
- [Over-Broad Scope](#over-broad-scope)
- [No Validation Path](#no-validation-path)
- [Wrong Agent Fit](#wrong-agent-fit)
- [Excessive Process](#excessive-process)
- [Few-Shot Without Boundaries](#few-shot-without-boundaries)

## Role Decoration Without Operational Value

Weak:

> You are a world-class expert.

Why it fails: role labels do little when the prompt does not define the work.

Fix:

- Replace generic role claims with concrete responsibilities, decision rules, and quality criteria.
- Keep role only when it changes voice, audience, or domain expectations.

## Vague Quality Words

Weak:

> Make it better, professional, robust, and high quality.

Why it fails: the agent cannot infer which tradeoff matters.

Fix:

- Define quality in observable terms: fewer steps, clearer copy, passing tests, cited claims, no layout overlap, lower latency, consistent schema.

## No Output Contract

Weak:

> Analyze this and tell me what you think.

Why it fails: the agent may return a generic essay when the user needs a table, patch, memo, JSON, checklist, or recommendation.

Fix:

- Specify format, sections, length, language, schema, and whether the output should be copy-ready.

## Hidden Assumptions

Weak:

> Build the best dashboard for sales.

Why it fails: the agent must invent user, metrics, data source, and workflow.

Fix:

- Ask clarification when assumptions change the task.
- If proceeding, add an `Assumptions` section and tell the agent to validate or state them.

## Context and Instructions Mixed Together

Weak:

> We use React and customers complain about onboarding so check the repo and make the page better maybe use our style.

Why it fails: facts, constraints, and tasks blur together.

Fix:

- Separate `Context`, `Inputs`, `Scope`, `Workflow`, and `Output Requirements`.

## Over-Broad Scope

Weak:

> Refactor the whole app to improve performance.

Why it fails: the agent may create a large risky diff without a success measure.

Fix:

- Define target area, non-goals, acceptable change size, and validation metric.

## No Validation Path

Weak:

> Fix the bug.

Why it fails: the agent can assert completion without evidence.

Fix:

- Add tests, reproduction steps, build commands, screenshots, citations, row checks, or acceptance criteria.

## Wrong Agent Fit

Weak:

> Browse the web and edit the repo.

Why it fails: not all agents can browse or edit files.

Fix:

- Adapt to the named agent. If capability is unknown, write capability-neutral instructions or tell the agent to report missing access.

## Excessive Process

Weak:

> First write a detailed plan, then wait, then create a framework, then produce three alternatives, then self-critique, then...

Why it fails: the prompt burns effort on process instead of the result.

Fix:

- Keep only process steps that reduce risk or improve correctness.
- For simple tasks, use a compact prompt.

## Few-Shot Without Boundaries

Weak:

> Here are examples. Do something like this.

Why it fails: the agent may copy incidental details or ignore label boundaries.

Fix:

- Explain what the examples demonstrate.
- Add decision rules and counterexamples for classification/extraction tasks.
