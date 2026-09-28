# Project Index

Updated: 2026-09-28
Coverage: Top-level skill inventory inspected; project-memory instructions read and updated. Other skill internals remain unmapped.

## Module map
| Area | Responsibility | Entry paths / key symbols | Related tests / configuration |
| --- | --- | --- | --- |
| Project memory | Cross-session context and reusable code lookup | project-memory/SKILL.md | project-memory/agents/agent.yaml |
| Requirements | Requirement clarification | requirements-clarifier/SKILL.md | requirements-clarifier/agents/agent.yaml |
| GitHub research | Research reusable implementations | github-code-research/SKILL.md | github-code-research/agents/agent.yaml |
| UI design | UI design guidance | ui-design/SKILL.md | ui-design/agents/agent.yaml |
| Skillshare | Skillshare management guidance | skillshare/SKILL.md | Not inspected |

## Task and bug lookup
| Feature / symptom / search terms | Implementation paths / symbols | Related flow / tests | Findings / verification |
| --- | --- | --- | --- |
| Memory init, project index, lookup, bug history | project-memory/SKILL.md: Initialize the project index; Locate before changing logic or fixing bugs | Memory location; When to update | Initialize module map, lookup first, targeted discovery on misses, repair stale entries; reviewed 2026-09-28. No executable runtime. |
