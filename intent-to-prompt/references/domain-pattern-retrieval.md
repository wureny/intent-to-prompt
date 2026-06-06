# Domain Pattern Retrieval

Use this when the task needs domain-specific prompt depth. The goal is not to find a prompt to copy. The goal is to retrieve or infer domain patterns that change how the final agent prompt should define workflow, constraints, schema, validation, source requirements, examples, or safety boundaries.

## Contents

- [Core Rule](#core-rule)
- [Depth Levels](#depth-levels)
- [Assessment Signals](#assessment-signals)
- [Retrieval Priorities](#retrieval-priorities)
- [What To Extract](#what-to-extract)
- [How To Integrate](#how-to-integrate)
- [When Not To Retrieve](#when-not-to-retrieve)
- [Examples](#examples)

## Core Rule

After classifying the task, decide whether generic prompt structure is enough. This is a judgment call, not a keyword trigger.

Activate domain depth when domain knowledge would materially change one or more of:

- workflow
- constraints
- output schema
- examples
- validation
- source requirements
- risk handling
- stop conditions
- success criteria

Do not activate domain depth just because the topic has a named field. Use it when the final prompt would be shallow, risky, or under-specified without domain patterns.

## Depth Levels

### None

Use when the task is simple, low-risk, and the existing task module is enough.

Example:

> Write a prompt for ChatGPT to summarize my meeting notes.

### Light

Use when the task benefits from domain-aware checks, but current knowledge is sufficient and the facts are not highly time-sensitive.

Example:

> Write a prompt for an agent to analyze SaaS churn.

Likely additions:

- cohort definitions
- retention vs churn metric definitions
- segmentation
- data quality checks
- correlation vs causation caveat

### Deep

Use when authoritative or current sources should shape the prompt.

Example:

> Write a prompt for Codex to audit our Kubernetes deployment configuration.

Likely additions:

- official Kubernetes docs or security guidance
- workload, network, RBAC, secret, resource, and probe checks
- severity rating
- false positive handling
- validation commands and stop conditions

## Assessment Signals

Use domain depth when the task has one or more strong signals:

- **Implicit professional standards**: security review, data analysis, legal extraction, medical summarization, financial analysis, compliance, hiring evaluation, incident response
- **Specific platform/tool dependence**: Kubernetes, Stripe, BigQuery, Salesforce, Figma, LangGraph, OpenAI API, Next.js, Terraform, dbt, Snowflake
- **High cost of error**: production systems, customer data, money, contracts, health, legal exposure, executive decisions
- **Need for domain validation**: tests, citations, metric reconciliation, schema validation, threat modeling, accessibility checks, regulatory checks
- **Hidden workflow**: experts in the field would follow a known process the user did not spell out
- **Reusable prompt**: the prompt will be embedded in a product, team workflow, classifier, extractor, evaluator, or automation

Explicit user requests like "use official best practices" or "make this production-grade" are strong signals, but they are not required.

## Retrieval Priorities

When Deep is needed and tools allow retrieval, prefer sources in this order:

1. Official documentation, API docs, developer guides, product docs
2. Official cookbooks, examples, reference implementations, release notes
3. Standards bodies, regulators, security benchmarks, professional guidelines
4. Maintainer-authored posts, high-quality engineering blogs, framework docs
5. Community prompts or examples, only as low-confidence inspiration

For OpenAI, cloud services, SDKs, APIs, frameworks, or libraries, prefer current official documentation.

For time-sensitive domains, require current sources and dates.

## What To Extract

Do not copy long prompts. Extract patterns:

- canonical workflow
- required inputs
- output schema
- quality criteria
- validation checks
- common failure modes
- edge cases
- safety or approval boundaries
- examples or counterexamples
- terminology the target agent must use precisely

Convert retrieved material into prompt structure. Keep citations or source notes only when the final prompt asks the target agent to research or when the user wants source-backed prompt design.

## How To Integrate

For Light depth:

- Add concise domain-specific checks to `Workflow`, `Quality Bar`, or `Validation`.
- Ask clarification only if a missing domain detail changes the prompt.
- Keep the prompt compact.

For Deep depth:

- If retrieval tools are available, retrieve authoritative sources before writing the final prompt.
- If retrieval tools are not available, write a prompt that instructs the target agent to retrieve official/current domain guidance before acting.
- Distinguish assumptions from sourced patterns.
- Add stop conditions for high-risk or external-impact tasks.

Useful final-prompt clause:

```markdown
Before acting, inspect authoritative domain guidance relevant to this task. Prefer official documentation and current sources. Use those sources to refine the workflow, checks, output schema, and validation criteria before producing the final result.
```

Use this clause only when the target agent can retrieve sources or the user wants the target agent to do the retrieval.

## When Not To Retrieve

Do not retrieve when:

- the user explicitly wants a fast draft and the task is low-risk
- the task is about personal preference or style and examples matter more than external sources
- the named domain does not change execution behavior
- the target agent cannot browse and the prompt can safely state assumptions
- retrieval would add latency without changing workflow, schema, validation, or risk handling

## Examples

### Coding: Kubernetes Audit

Raw intent:

> Make a prompt for Codex to review our Kubernetes deployment.

Depth: Deep.

Why:

- specific platform
- production risk
- hidden expert workflow
- validation and safety boundaries matter

Prompt additions:

- inspect manifests and deployment tooling
- review RBAC, secrets, resource requests/limits, probes, security context, image tags, network policy
- cite or follow official/current Kubernetes security guidance if browsing is available
- produce findings by severity with file references and remediation steps
- ask before applying broad changes

### Data: SaaS Churn Analysis

Raw intent:

> Write a prompt for an agent to analyze why churn increased.

Depth: Light or Deep depending on data/source complexity.

Prompt additions:

- define churn metric and observation window
- check cohorts, segments, plan mix, billing status, seasonality, instrumentation changes
- separate correlation from causation
- validate row counts and metric reconciliation
- produce hypotheses with evidence strength and next analyses

### Product-Embedded: Support Classifier

Raw intent:

> Create a prompt to classify support tickets.

Depth: Light.

Prompt additions:

- allowed labels
- label definitions
- JSON output schema
- confidence and escalation behavior
- borderline examples and tie-break rules
- avoid inventing labels

### Legal/Contract Extraction

Raw intent:

> Make a prompt to extract risky clauses from vendor contracts.

Depth: Deep if used for real decisions.

Prompt additions:

- clarify jurisdiction and contract type
- extract clauses with quote, location, risk category, explanation, and uncertainty
- avoid legal advice beyond extraction unless reviewed by counsel
- include human review requirement
- use examples for clause categories if provided
