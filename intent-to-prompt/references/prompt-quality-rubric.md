# Prompt Quality Rubric

Use this rubric silently unless the user asks for a diagnosis. It guides whether to ask clarification questions, make assumptions, or produce the final prompt.

## Scoring

Score each dimension 0-2:

- **0**: missing or dangerously vague
- **1**: present but incomplete
- **2**: clear enough for execution

A prompt is usually ready at 14+ total points if no critical dimension is 0. Ask clarification when a critical dimension is 0 and cannot be safely assumed.

## Dimensions

1. **Objective clarity**
   - 0: "help me improve this"
   - 1: "improve the onboarding page"
   - 2: "redesign the onboarding page to increase first-session activation"

2. **Context sufficiency**
   - Includes background, audience, project state, constraints, or why the task matters.

3. **Input boundaries**
   - Specifies files, links, data, text, screenshots, examples, or source materials the agent should use.

4. **Scope control**
   - Says what to do and what not to do. Important for coding, design, and automation.

5. **Constraints**
   - Captures style, tech stack, timeline, budget, policy, data, privacy, compatibility, or platform constraints.

6. **Workflow guidance**
   - Indicates whether the agent should first inspect, ask, plan, research, implement, compare options, or act directly.

7. **Output contract**
   - Defines deliverable format: patch, report, table, JSON, checklist, PR description, slide outline, etc.

8. **Quality bar**
   - Defines what "good" means: accuracy, readability, minimal changes, evidence, performance, UX, tone, completeness.

9. **Validation criteria**
   - Includes tests, checks, citations, screenshots, edge cases, acceptance criteria, or review standards.

10. **Risk and uncertainty handling**
    - Defines when to ask for approval, when to state assumptions, how to handle missing info, and what actions are off-limits.

## Critical Missing Information

Ask before producing a final prompt when any of these are missing and materially affect execution:

- target agent or capability assumptions are unclear
- final deliverable is unclear
- editable scope is unclear for coding/design/file tasks
- source of truth is unclear for research/data tasks
- audience or tone is unclear for high-stakes writing
- success criteria are unclear for tasks that need validation
- permissions are unclear for irreversible, expensive, external, or destructive actions

## Diagnosis Patterns

**Vague objective**

- Symptom: many reasonable outputs would satisfy the request.
- Upgrade: force a concrete outcome and definition of done.

**Missing context**

- Symptom: agent would need to infer project, audience, constraints, or source material.
- Upgrade: add background and "use these inputs" section.

**No output contract**

- Symptom: agent may produce prose when user needs code, table, JSON, or steps.
- Upgrade: specify exact final format.

**No validation**

- Symptom: agent can claim completion without proof.
- Upgrade: add tests, checks, citations, screenshots, or acceptance criteria.

**Over-broad scope**

- Symptom: agent may refactor unrelated files, research forever, or redesign too much.
- Upgrade: add non-goals and stopping conditions.

**Premature prompt**

- Symptom: final prompt would be mostly assumptions.
- Upgrade: ask 1-3 questions before writing.

## Readiness Actions

- **Ready**: produce final prompt.
- **Almost ready**: produce final prompt with explicit assumptions.
- **Not ready**: ask clarifying questions only.
- **High risk**: ask permission/scope questions first; include stop conditions in the final prompt.
