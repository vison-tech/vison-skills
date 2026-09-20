---
name: project-memory
description: Maintain a concise, project-local memory file so a new Codex session can quickly recover the current state, decisions, commands, blockers, and next steps. Use during coding, debugging, reviews, and project planning; do not create memory for one-off non-project questions.
---

# Project Memory

Keep durable project context close to the repository and update it as part of
normal engineering work. This is a prompt-level workflow, not a background
filesystem watcher: make the read/update actions explicitly during relevant
tasks.

## Memory location

Use the first applicable path:

1. `.codex/project-memory.md` at the project root (preferred).
2. `PROJECT_MEMORY.md` at the project root when `.codex` is unavailable or the
   project convention uses a root-level file.

If neither exists, create `.codex/project-memory.md` only when the project is
under version control or the user has clearly asked for project memory. Do not
create a memory file in a general notes folder for a repository task.

## At the start of a relevant task

Read the memory file before planning or changing code. Treat it as context, not
ground truth: verify important claims against the working tree, configuration,
tests, and recent history. Also inspect `git status` when available so the
memory does not cause unrelated user changes to be overwritten.

If the file is missing, continue normally and create it after the first
meaningful project change or when the user asks for a status snapshot.

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
