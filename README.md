# intent-to-prompt

`intent-to-prompt` is a Codex skill that converts rough user intent into precise, complete, agent-ready prompts.

It helps an AI agent decide when to ask clarification questions, when to proceed with assumptions, and how to produce prompts with clear objective, context, scope, workflow, output requirements, quality bar, validation, examples, and target-agent adaptation.

## What It Does

- Turns vague task intent into copy-ready prompts for AI agents.
- Asks only high-value clarification questions before writing the final prompt.
- Supports Quick Prompt, Agent Prompt, and Product Prompt modes.
- Adapts prompts for Codex, Claude Code, Gemini CLI, ChatGPT, research agents, product-embedded prompts, image/video models, and automation agents.
- Uses prompt quality rubrics, anti-pattern checks, few-shot strategy, and validation loops.

## Supported Scenarios

- Coding agent prompts
- Research prompts
- Writing prompts
- Data analysis prompts
- Design and prototype prompts
- Image/video prompts
- Product-embedded reusable prompts
- Automation agent prompts

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R intent-to-prompt ~/.codex/skills/
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
