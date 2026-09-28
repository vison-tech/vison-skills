# Project Memory

Updated: 2026-09-28

## Current state
- Updated project-memory to initialize and incrementally maintain a project index, with lookup before logic changes and bug fixes.

## Architecture and conventions
- This repository stores reusable skills in named directories containing SKILL.md and optional agents metadata.
- Project index: [Project Index](project-index.md).
- Codex's installed project-memory symlink points to /Users/vison/.config/skillshare/skills/project-memory, a separate copy from this repository.

## Decisions
- Keep project status in memory and implementation lookup in a separate index; initialize a module map once, then enrich affected entries as tasks proceed — 2026-09-28.

## Commands and verification
- `git diff --check` passed after the skill edit.
- Bundled `quick_validate.py project-memory` could not run: system Python lacks PyYAML.

## Blockers and risks
- Installed copies can diverge from repository sources; verify synchronization when editing skills.

## Next steps
- Observe index reuse in subsequent project tasks and refine only when actual gaps appear.
