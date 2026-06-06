# intent-to-prompt

`intent-to-prompt` is a Codex skill that turns rough intent into precise, complete, agent-ready prompts.

It is useful when you know what you want an AI agent to do, but your request is still too vague, underspecified, or hard for an agent to execute reliably.

Instead of only polishing wording, this skill treats prompt engineering as task specification: it clarifies the goal, context, scope, workflow, output format, quality bar, validation path, examples, and target-agent assumptions.

## Who This Is For

Use this skill if you:

- use Codex, Claude Code, Gemini CLI, ChatGPT, or other AI agents for real work
- often write prompts like "help me improve this", "fix this", "research this", or "build this"
- want agents to ask better clarification questions before acting
- want fewer vague outputs, fewer wrong assumptions, and less back-and-forth
- are building reusable prompts for a product, internal workflow, or team process
- care about prompt quality, but do not want to manually apply prompt-engineering checklists every time

## When To Use It

Use `intent-to-prompt` before handing work to an agent when the task needs clear execution behavior:

- **Coding**: ask Codex or Claude Code to debug, refactor, build, review, or test something
- **Research**: ask an agent to compare tools, synthesize sources, or produce a decision memo
- **Writing**: draft or rewrite docs, emails, PRDs, strategy memos, essays, or launch copy
- **Data analysis**: define metrics, analyze datasets, build dashboards, or write analytical reports
- **Design**: create product flows, prototypes, UI prompts, or design review instructions
- **Image/video**: convert visual intent into concrete generation/editing prompts
- **Reusable prompts**: design prompts embedded in products, support workflows, classifiers, extractors, or automations

Do not use it for tiny one-off questions where a direct answer is enough.

## What It Does

- Turns vague task intent into copy-ready prompts for AI agents.
- Asks only high-value clarification questions before writing the final prompt.
- Supports Quick Prompt, Agent Prompt, and Product Prompt modes.
- Adapts prompts for Codex, Claude Code, Gemini CLI, ChatGPT, research agents, product-embedded prompts, image/video models, and automation agents.
- Uses prompt quality rubrics, anti-pattern checks, few-shot strategy, and validation loops.

## How It Works

The skill follows a practical prompt-engineering workflow:

1. Classify the task type.
2. Decide whether to ask clarification questions or proceed with assumptions.
3. Select the right prompt mode: Quick Prompt, Agent Prompt, or Product Prompt.
4. Build a draft prompt with objective, context, scope, workflow, output requirements, and validation.
5. Adapt the prompt to the target agent or tool.
6. Add examples, schemas, source requirements, stop conditions, or validation loops when they improve execution.
7. Review and revise once to remove common prompt anti-patterns.

## Quick Start

Install with the Agent Skills CLI:

```bash
npx skills add wureny/intent-to-prompt --skill intent-to-prompt -a codex -g -y
```

Then restart Codex or start a new thread.

## Usage

```text
Use intent-to-prompt to turn this intent into a high-quality prompt for Codex:
I want an agent to fix the flaky checkout test in my repo.
```

```text
Use intent-to-prompt to improve this prompt for a research agent:
Research whether we should use LangGraph or build our own orchestration layer.
```

```text
Use intent-to-prompt to create a reusable product prompt:
Classify support tickets into billing, bug, feature request, or account access.
```

## Before and After

Rough intent:

```text
I want Codex to improve the login page.
```

What `intent-to-prompt` does first:

```text
1. What should "improve" mean here: visual polish, conversion, accessibility, mobile layout, performance, or a specific bug?
2. Can the agent change only the login page, or also shared components/styles?
3. How should the agent validate the result: tests, screenshot review, browser QA, or specific acceptance criteria?
```

For a clearer task, it produces a copy-ready agent prompt with sections like:

```text
# Objective
# Context
# Scope
# Workflow
# Output Requirements
# Quality Bar
# Validation
```

## Alternative Install Methods

### From Inside Codex

You can also ask Codex to install the skill from this GitHub directory:

```text
$skill-installer install https://github.com/wureny/intent-to-prompt/tree/main/intent-to-prompt
```

Restart Codex after installation.

### Manual Install

If you prefer not to use `npx`, copy the installable skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R intent-to-prompt ~/.codex/skills/
```

Restart Codex after installation.

## Example Behavior

If the user intent is missing critical details, the skill asks concise clarification questions first.

If the intent is clear enough, it produces a final agent prompt directly.

If the user wants speed, it proceeds with explicit assumptions.

## Repository Structure

```text
intent-to-prompt/
  README.md
  LICENSE
  intent-to-prompt/
    SKILL.md
    agents/
      openai.yaml
    references/
      ...
```

The inner `intent-to-prompt/` directory is the installable Codex skill.

## License

MIT
