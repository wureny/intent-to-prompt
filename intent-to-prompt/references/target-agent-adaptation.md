# Target Agent Adaptation

Use this when the user names a target agent or when the execution environment materially changes the prompt.

## Contents

- [Agent-Neutral Default](#agent-neutral-default)
- [Codex or Claude Code](#codex-or-claude-code)
- [Gemini CLI or Terminal Coding Agents](#gemini-cli-or-terminal-coding-agents)
- [ChatGPT or General Chat Assistants](#chatgpt-or-general-chat-assistants)
- [Research Agents](#research-agents)
- [Product-Embedded Prompts](#product-embedded-prompts)
- [Image and Video Models](#image-and-video-models)
- [Automation Agents](#automation-agents)

## Agent-Neutral Default

Use when the user wants broad compatibility.

Prefer:

- capability-neutral verbs: "inspect available context", "use available tools", "report missing access"
- explicit objective, scope, output, and validation
- stop conditions for risky actions

Avoid:

- naming tools the agent may not have
- assuming file write access, browsing, shell, plugins, or API credentials

## Codex or Claude Code

Use for repository-aware coding agents.

Emphasize:

- read the codebase before editing
- follow existing patterns
- make scoped changes
- do not revert unrelated user changes
- use patch/edit tools carefully
- run tests, type checks, lint, build, or targeted commands
- summarize files changed and validation

Add when frontend:

- run or inspect the app if possible
- verify responsive layout and visual states
- use screenshots/browser checks where available

Avoid:

- asking for long plans when the task is straightforward
- telling the agent to use specific commands unless known from the project
- broad rewrites without acceptance criteria

## Gemini CLI or Terminal Coding Agents

Use for coding agents with shell-centric workflows.

Emphasize:

- inspect files with fast search tools when available
- avoid destructive shell commands unless explicitly approved
- prefer targeted tests and reproducible commands
- report command failures and environment blockers

Avoid:

- assuming an interactive browser or IDE integration
- relying on visual inspection unless the agent has that capability

## ChatGPT or General Chat Assistants

Use when the target may not edit files or run tools.

Emphasize:

- ask clarifying questions when needed
- provide structured reasoning summaries without hidden chain-of-thought
- produce copy-ready text, plans, checklists, or code snippets
- state assumptions and limitations

Avoid:

- tool-dependent instructions like "run tests" unless the user will execute them
- repository mutation instructions if the assistant cannot edit files

## Research Agents

Use when the agent can browse or retrieve sources.

Emphasize:

- source hierarchy: official, primary, recent, credible secondary
- dates for time-sensitive facts
- citations and links
- fact vs inference separation
- confidence and uncertainty

Avoid:

- vague "research deeply" instructions
- source-free recommendations
- over-reliance on summaries when primary sources are available

## Product-Embedded Prompts

Use for prompts that will run repeatedly inside an application.

Emphasize:

- input variables and meanings
- output schema
- examples and counterexamples
- refusal/fallback behavior
- deterministic style and label boundaries
- evaluation checks

Avoid:

- conversation-specific context
- hidden dependencies on the current user
- open-ended output when downstream code expects structure

## Image and Video Models

Use for visual generation/editing prompts.

Emphasize:

- concrete visible elements
- composition, framing, camera, lighting, palette, medium
- aspect ratio and output variants
- what must remain unchanged for edits
- negative constraints for unwanted elements

Avoid:

- abstract-only goals like "make it inspiring"
- long narrative context that does not affect pixels
- conflicting style references

## Automation Agents

Use when the agent will operate tools or external systems over multiple steps.

Emphasize:

- mission and success criteria
- permission boundaries
- reversible steps first
- approval checkpoints
- failure handling
- concise action log
- stop conditions

Avoid:

- granting broad implied permission
- external side effects without confirmation
- vague "keep going until done" instructions
