---
name: project-memory
description: Maintain concise project-local memory and a reusable code index so later sessions can recover context and locate implementation without repeatedly scanning the repository. Use during coding, debugging, reviews, and project planning; do not create memory for one-off non-project questions.
---

# Project Memory

Keep durable project context close to the repository and update it as part of
normal engineering work. This is a prompt-level workflow, not a background
filesystem watcher: make the read/update actions explicitly during relevant
tasks.

## Execution priority

This skill should execute **first** in the skill chain, before other skills like
`requirements-clarifier`, `ui-design`, or `github-code-research`. Always load
existing project memory at the start of a new task to provide context for
subsequent clarification and implementation steps.

## Memory location

Use the first applicable path:

1. `.memory/project-memory.md` at the project root (preferred).
2. `PROJECT_MEMORY.md` at the project root when `.memory` is unavailable or the
   project convention uses a root-level file.

If neither exists, create `.memory/project-memory.md` only when the project is
under version control or the user has clearly asked for project memory. Do not
create a memory file in a general notes folder for a repository task.

## At the start of a relevant task

Read the memory file before planning or changing code. Treat it as context, not
ground truth: verify important claims against the working tree, configuration,
tests, and recent history. Also inspect `git status` when available so the
memory does not cause unrelated user changes to be overwritten.

If the file is missing, continue normally and create it after the first
meaningful project change or when the user asks for a status snapshot.

## Initialize the project index

On first memory initialization, also create `.memory/project-index.md` and
link it from the memory file. If the project uses root-level memory because
`.memory` is unavailable, use `PROJECT_INDEX.md` beside `PROJECT_MEMORY.md`.
For existing memory without an index, build the index on the next relevant
task. Respect existing equivalent indexes instead of creating duplicates.

Build a useful project map once: inspect the file tree with `rg --files`,
project documentation, manifests, and representative entry points. Identify
major modules, their responsibilities, runtime entry points, configuration,
and test/build locations. Exclude dependencies, generated output, caches,
and vendored code unless directly relevant. Do not read every source file or
claim complete coverage; mark areas that have not yet been inspected.

Keep a compact module directory and task lookup table:

```markdown
# Project Index

Updated: YYYY-MM-DD
Coverage: Areas inspected and areas still unmapped.

## Module map
| Area | Responsibility | Entry paths / key symbols | Related tests / configuration |
| --- | --- | --- | --- |

## Task and bug lookup
| Feature / symptom / search terms | Implementation paths / symbols | Related flow / tests | Findings / verification |
| --- | --- | --- | --- |
```

Use repository-relative paths and stable symbol names; line numbers are
optional hints, never the sole locator. Include the date or commit of
verification for entries. Link larger module notes only when needed and
load only notes relevant to the task; keep source code in the source files.

## Locate before changing logic or fixing bugs

1. Read project memory and search the index for the feature, symptom, module,
   and known aliases before searching repository-wide.
2. Follow matching paths and symbols. Verify that they still exist and inspect
   the relevant implementation and tests before relying on previous findings.
   Treat indexed bug causes as historical context, not proof of the current cause.
3. If an entry is missing, stale, or insufficient, search the likely module
   first using `rg` and inspect the related call chain. Widen the search only
   as needed. Once the implementation is located, add or repair its index entry
   before continuing the change; record only verified findings and label open
   questions. A missing index entry must not block the actual task.
4. After the change or fix, update the affected entries with the resulting
   behavior, confirmed root cause when applicable, and regression test or
   verification command and observed result. Remove obsolete paths and findings.

Reuse unaffected entries. Do not rebuild the index or scan all code on every
task. Broader discovery is appropriate when targeted lookup fails or major
restructuring makes the map unreliable; refresh only affected areas where possible.

## What to record

Keep the file short and scannable. Preserve this structure unless an existing
project convention requires another one:

```markdown
# Project Memory

Updated: YYYY-MM-DD

## Current state
- What works and what is in progress.

## Architecture and conventions
- Important modules, data flow, interfaces, and project-specific rules.
- Project index: [Project Index](project-index.md).

## Decisions
- Decision — reason — date (or commit/issue if useful).

## Commands and verification
- Reliable setup, test, build, and deployment commands.

## Blockers and risks
- Known failures, compatibility concerns, or unresolved questions.

## Next steps
- The smallest useful follow-up actions.
```

Record facts that will remain useful across sessions: completed work, current
implementation status, key design decisions, dependency or schema changes,
verification results, known blockers, and explicit next steps. Mark uncertain
items as hypotheses or questions instead of presenting them as facts.

## When to update

Update the memory in the same task after a meaningful change, such as:

- changing architecture, public APIs, data models, dependencies, or scripts;
- discovering the cause of a bug or a reliable workaround;
- completing a feature, migration, review, or verification run;
- encountering a blocker that changes what should happen next.

Do not update for every file edit or transient tool output. Before writing,
re-read the existing file and merge the new facts; do not replace useful context
with a session transcript. Remove stale statements and keep “Next steps” honest.
Update the affected index entries in the same task when files, symbols,
responsibilities, or call paths change. Keep detailed lookup information in
the index and concise project status in memory; avoid duplicating both.

## Safety and scope

- Never record passwords, API keys, access tokens, private URLs, personal data,
  or full secret-bearing command lines. Describe the existence of a secret or
  configuration requirement without its value.
- Do not claim tests, builds, deployments, or external actions succeeded unless
  they were actually observed. Include failures and relevant error summaries.
- Do not modify `.gitignore`, commit the memory file, or change repository
  history unless the user asks. Follow existing repository conventions when
  they already define whether `.codex` files are tracked.
- If the repository has no writable location for memory, report that limitation
  and provide the proposed snapshot in the response instead of inventing a
  hidden store.
