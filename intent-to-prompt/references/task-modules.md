# Task Modules

Load only the relevant module. Combine modules when the task is truly hybrid, such as coding plus research or data analysis plus writing.

## Contents

- [Coding Agent Module](#coding-agent-module)
- [Research Module](#research-module)
- [Writing Module](#writing-module)
- [Data Analysis Module](#data-analysis-module)
- [Design and Prototype Module](#design-and-prototype-module)
- [Image and Video Module](#image-and-video-module)
- [Automation Agent Module](#automation-agent-module)
- [General Assistant Module](#general-assistant-module)

## Coding Agent Module

Use for software engineering agents that can inspect files, edit code, and run commands.

Add sections for:

- repository context and target area
- task objective
- files/modules likely in scope
- constraints: minimal changes, preserve existing behavior, follow local patterns
- workflow: inspect first, plan briefly, implement, test, summarize
- safety: do not overwrite unrelated user changes; ask before destructive operations
- validation: unit tests, type checks, lint, build, manual QA, screenshots when frontend
- final response: changed files, verification, residual risks

Useful prompt clauses:

- "Read the existing code before proposing changes."
- "Prefer existing project patterns over new abstractions."
- "Keep changes scoped to the requested behavior."
- "Do not revert unrelated user changes."
- "Run the narrowest meaningful tests, then broader checks if the change touches shared behavior."
- "If tests cannot be run, explain why and provide the strongest available verification."

## Research Module

Use for web, document, market, technical, legal, financial, or competitive research.

Add sections for:

- research question and decision context
- source requirements: primary sources, official docs, recent sources, citations
- time sensitivity and geographic scope
- methodology: search, compare, cross-check, synthesize
- evidence standards: distinguish fact, inference, and uncertainty
- output: brief, table, memo, recommendations, annotated bibliography
- validation: cite sources, note dates, flag weak evidence

Useful prompt clauses:

- "Use current sources where facts may have changed."
- "Prioritize primary sources and official documentation."
- "Separate sourced facts from your analysis."
- "Include links and publication/access dates where relevant."
- "Do not overstate confidence when evidence is thin."

## Writing Module

Use for memos, essays, emails, posts, PRDs, narratives, strategy docs, scripts, and communication.

Add sections for:

- audience
- purpose and desired reader action
- tone and voice
- source material and claims to preserve
- structure
- length
- examples or style references
- revision mode: draft from scratch, improve, rewrite, critique

Useful prompt clauses:

- "Preserve the author's core intent while improving clarity and force."
- "Use concrete examples rather than generic claims."
- "Avoid jargon unless the audience expects it."
- "Make the conclusion actionable."
- "If information is missing, mark placeholders instead of inventing facts."

Few-shot is especially useful for voice, style, classification, extraction, and recurring formats.

## Data Analysis Module

Use for spreadsheets, SQL, metrics, dashboards, notebooks, and analytical reports.

Add sections for:

- business question
- datasets and schemas
- metric definitions
- filters, date ranges, cohorts, and grain
- expected output: chart, table, notebook, dashboard, memo
- reproducibility requirements
- validation: row counts, null checks, reconciliation, sanity checks
- caveats: sampling, missing data, access limits

Useful prompt clauses:

- "State metric definitions before calculating."
- "Check data quality before interpreting results."
- "Use reproducible queries or formulas."
- "Separate observed results from causal explanations."
- "Include caveats where data cannot support the conclusion."

## Design and Prototype Module

Use for UI/UX, product design, flows, prototypes, visual QA, and design critique.

Add sections for:

- target user and primary workflow
- product/domain context
- existing design system or visual constraints
- required screens/states
- interaction expectations
- responsive behavior
- accessibility and usability checks
- validation: screenshots, browser checks, edge states, no overlap/clipping

Useful prompt clauses:

- "Build the actual usable experience, not a landing page, unless requested."
- "Follow the existing design system and component patterns."
- "Design for the user's repeated workflow, not only first impression."
- "Verify desktop and mobile layouts."
- "Check for text overflow, overlap, empty states, loading states, and error states."

## Image and Video Module

Use for prompts sent to image/video generation or editing systems.

Add sections for:

- subject
- purpose and audience
- composition and framing
- medium/style
- setting, lighting, color, mood
- required details
- negative constraints
- aspect ratio/resolution
- references
- output variants

Useful prompt clauses:

- "Describe observable visual details, not abstract intent alone."
- "Specify composition, subject placement, and camera/framing."
- "Include constraints for text rendering, logos, hands, faces, or brand accuracy when relevant."
- "For edits, state what must remain unchanged."

## Automation Agent Module

Use for agents that will operate tools over multiple steps, especially with external systems.

Add sections for:

- mission and success criteria
- available tools and credentials assumptions
- permission boundaries
- step order
- checkpoints requiring user approval
- failure handling
- logging and final report
- stop conditions

Useful prompt clauses:

- "Before any irreversible, costly, or external action, stop and ask for approval."
- "Keep a concise action log."
- "If blocked by missing access, report exactly what access is needed."
- "Prefer reversible operations and dry runs first."

## General Assistant Module

Use when no specialized module fits.

Add sections for:

- objective
- context
- constraints
- output format
- quality bar
- assumptions

Keep the prompt compact.
