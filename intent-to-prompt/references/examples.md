# Examples

Use these examples to calibrate behavior. Do not copy them mechanically.

## Contents

- [Example 1: Coding Task Needs Clarification](#example-1-coding-task-needs-clarification)
- [Example 2: Coding Task With Assumptions](#example-2-coding-task-with-assumptions)
- [Example 3: Research Prompt](#example-3-research-prompt)
- [Example 4: Reusable App Prompt Needs Few-Shot](#example-4-reusable-app-prompt-needs-few-shot)
- [Example 5: Design Prompt](#example-5-design-prompt)

## Example 1: Coding Task Needs Clarification

Raw intent:

> Help me tell Codex to improve the login page.

Response:

```markdown
## Clarifying Questions

1. What should "improve" mean here: visual polish, conversion, accessibility, mobile layout, performance, or a specific bug?
2. Can the agent change only the login page, or also shared components/styles?
3. How should the agent validate the result: tests, screenshot review, browser QA, or specific acceptance criteria?
```

## Example 2: Coding Task With Assumptions

Raw intent:

> Write a prompt for Codex to fix the flaky checkout test. Assume it can inspect the repo.

Response:

```markdown
## Assumptions

- The agent can read files, edit code, and run the project's test command.
- The goal is to fix the underlying flakiness, not simply loosen assertions.

## Final Agent Prompt

# Objective

Find and fix the flaky checkout test by identifying the root cause and making the smallest reliable code or test change.

# Context

The repository contains an existing checkout flow and at least one flaky test. The test failure may come from async timing, shared state, test isolation, mocked services, or nondeterministic data.

# Workflow

1. Inspect the failing test, related checkout code, test setup, mocks, and recent patterns in nearby tests.
2. Reproduce or reason through the flake before editing.
3. Fix the root cause with the smallest coherent change. Do not hide the problem with arbitrary sleeps or broad assertion weakening.
4. Run the failing test repeatedly if possible, then run the relevant surrounding test suite.
5. If reproduction is not possible, explain the evidence supporting the fix.

# Constraints

- Preserve checkout behavior unless the investigation proves a product bug.
- Follow existing test utilities and project style.
- Do not refactor unrelated checkout code.
- Do not revert unrelated user changes.

# Output Requirements

Summarize the root cause, changed files, validation commands and results, and any residual risk.
```

## Example 3: Research Prompt

Raw intent:

> I want an agent to research whether we should use LangGraph or build our own orchestration layer.

Response:

```markdown
## Final Agent Prompt

# Research Objective

Compare LangGraph with building an internal orchestration layer for an LLM agent product, and recommend which path to choose under explicit assumptions.

# Context

The decision concerns agent orchestration: state management, tool calls, retries, observability, human-in-the-loop workflows, maintainability, and production reliability.

# Scope

Include:
- LangGraph capabilities, ecosystem maturity, operational tradeoffs, and integration costs
- build-vs-buy considerations for a small engineering team
- migration and lock-in risks
- examples from official docs, credible engineering writeups, or source repositories

Exclude:
- generic LLM framework comparisons unless they affect the decision
- unsourced claims from low-quality summaries

# Source Requirements

- Prioritize official documentation, source repositories, release notes, and credible technical posts.
- Use current sources because framework capabilities change quickly.
- Cite links for material claims.
- Distinguish facts from your judgment.

# Output

Return a decision memo with:
1. recommendation
2. assumptions
3. comparison table
4. risks and mitigations
5. what to prototype before committing
```

## Example 4: Reusable App Prompt Needs Few-Shot

Raw intent:

> Create a prompt for classifying support tickets.

Good response asks first if labels, examples, and downstream use are missing. If labels are provided, include few-shot examples because classification depends on boundary calibration.

Final prompt should include:

- label definitions
- tie-break rules
- output JSON
- confidence or escalation field
- 3-5 labeled examples
- instruction to avoid inventing labels

## Example 5: Design Prompt

Raw intent:

> Make a prompt for an agent to build a dashboard for a sales manager.

Response should clarify data source and metrics if missing. If proceeding with assumptions, final prompt should include:

- target user: sales manager
- core workflow: scan pipeline health, identify risks, drill into reps/accounts
- required states: loading, empty, error
- visual style: dense, operational, not marketing-like
- validation: responsive screenshots, no text overlap, meaningful table/chart states
