---
name: github-code-research
description: Research relevant GitHub projects and implementations before building a reusable software capability, selecting a library, or recreating a common integration. Use for non-trivial implementation work where mature open-source code may save time; do not use for small project-specific edits or when the user explicitly wants a from-scratch implementation.
---

# Github Code Research

Find practical, compatible reuse opportunities without turning every change into
an internet-research task.

## Execution priority

This skill should execute **after** `project-memory` loads context and 
`requirements-clarifier` confirms the plan. Research decisions should be based 
on clarified requirements and existing project constraints.

## When to research

Before implementing, inspect the current repository's dependencies, conventions,
and existing capabilities. Research GitHub when the work could reasonably be
handled by an established library, SDK, integration, algorithm, component, or
reference implementation. Examples include authentication, payments, document
parsing, protocol clients, rich editors, schedulers, visualizations, AI tooling,
and non-trivial infrastructure.

Do not research for a narrow bug fix, simple glue code, domain-specific business
rules, or a task the user explicitly asks to implement from scratch. Do not
repeat a search that has already been performed in the current task unless the
requirements materially change.

## Research workflow

1. State the capability to evaluate and the important constraints: language,
   runtime, framework, license, deployment model, and security requirements.
2. Use an available GitHub integration, authenticated `gh` CLI, or GitHub's
   public interface to find a small set of relevant repositories. Prefer exact
   technology and problem terms over broad keyword searches.
3. Inspect the candidate's README, dependency manifest, recent maintenance,
   issue activity, license, release history, and the specific API or source
   needed for the proposed use. Do not treat star count as sufficient evidence.
4. Compare candidates against the repository's existing stack. Prefer adding a
   maintained, compatible dependency over copying source. Reuse a pattern from
   source only when its license, quality, and maintenance make that appropriate.
5. Summarize the decision concisely before implementation: candidate links,
   why the selected option fits, material tradeoffs, and whether the work will
   depend on, adapt, or avoid it. Then implement only the agreed scope.

## Constraints

- Do not install packages, clone repositories, publish code, or send GitHub
  requests that change remote state without the user's authorization.
- Respect repository licenses and attribution requirements. Avoid copying
  substantial code from copyleft, unclear, or incompatible licenses into a
  project unless the user explicitly approves that licensing consequence.
- Treat README claims and unverified examples as leads, not proof. Validate the
  exact API version and behavior relevant to the task.
- Keep retrieved code minimal. Adapt it to the local project's style and test
  the integration rather than importing an entire example application.
- If GitHub access is unavailable, say so briefly and proceed with local
  inspection and the best supported solution; do not invent search results.
