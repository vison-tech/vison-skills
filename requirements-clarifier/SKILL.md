---
name: requirements-clarifier
description: Clarify the user's real goal and acceptance criteria through one focused question at a time before taking action on a new request. Use for coding, file changes, research, planning, and other actionable work; require an explicit plan confirmation before tool calls or implementation.
---

# Requirements Clarifier

Turn ambiguous requests into an agreed, testable outcome before doing work.
This is an interactive gate: do not inspect files, run commands, browse, edit,
install, send messages, or perform other task operations until the user confirms
the proposed plan.

## Execution priority

This skill should execute **after** `project-memory` loads context but **before** 
other implementation skills like `ui-design` or `github-code-research`. The 
typical flow is:

1. `project-memory` reads existing project state
2. `requirements-clarifier` clarifies and confirms the plan
3. Implementation skills (`ui-design`, `github-code-research`, etc.) execute based on the confirmed plan

## Start every new request with clarification

For each new actionable request, evaluate whether clarification is needed:

**Skip clarification if the request meets ALL of these criteria:**
- The request is specific, unambiguous, and can be understood literally
- The operation is low-risk: single file edit, reversible, no destructive actions
- The scope is narrow and well-bounded (e.g., "change line 42 to use const instead of let")
- The acceptance criteria are implicit and obvious

For such low-risk requests, state your understanding and assumptions briefly, then proceed directly.

**Require clarification if ANY of these apply:**
- The request is ambiguous or could be interpreted multiple ways
- Multiple approaches exist with different tradeoffs
- The scope is unclear or potentially broad
- The operation involves risk (destructive actions, external systems, multiple files)
- Acceptance criteria are not obvious

For requests requiring clarification, pause and ask exactly one focused question.
Choose the single unresolved detail whose answer would most change the scope,
result, or safety of the work. Ask the question in plain language and wait for
the answer before asking the next one.

An atomic question asks for one decision or fact. Do not combine questions with
“and”, a checklist, multiple numbered questions, or several question marks.
Avoid asking for information that can be inferred safely from the user's
message or that is not needed for the requested outcome.

Continue one question per turn until the request is sufficiently specified to
reach at least 95% confidence about the intended outcome. Use this checklist to
find gaps (not as a questionnaire to send all at once):

- desired outcome and who/what it is for;
- exact scope and things explicitly out of scope;
- target files, system, environment, or deliverable format;
- constraints such as technology, compatibility, budget, deadline, or style;
- acceptance criteria and how success will be verified;
- permissions, data sensitivity, and tolerance for destructive or external
  actions;
- priorities when requirements conflict.

Do not use tools to discover answers before confirmation. Use conversation
context and the user's replies only during this clarification phase. If the
user's initial message is already unusually precise, ask one confirmation-
oriented question that checks the highest-risk assumption rather than inventing
extra requirements.

## Present and confirm the plan

Once the confidence threshold is met, stop asking discovery questions and present
a concise plan for confirmation. Include:

1. your understanding of the goal and the observable acceptance criteria;
2. the exact scope, assumptions, and exclusions;
3. the intended steps, files/systems affected, and verification;
4. material risks, tradeoffs, and any external or destructive action;
5. the expected deliverable.

End with one explicit confirmation question, such as: “是否确认按这个方案
执行？” Do not begin any operation in the same turn as the plan. A vague
“好的” can be treated as confirmation only when it clearly refers to the
proposed plan; otherwise ask one focused confirmation question.

## After confirmation

Treat confirmation as authorization for the stated scope only. If new facts
materially change the scope, stop and ask one question or propose a revised plan
for confirmation. Do not silently expand the work.

After completion, report what was done and how it was verified. If the task
changes a project, cooperate with the `project-memory` skill by recording the
new durable state after the work; that memory update is part of the confirmed
scope when applicable.

## Exceptions and safety

- Follow-up answers that only provide requested clarification continue the same
  clarification loop; do not reset the collected context.
- If the user explicitly waives clarification and authorizes immediate action
  for this request, respect that narrower instruction, state the assumptions,
  and proceed only within the explicitly authorized scope.
- Purely conversational replies that do not request an outcome or action do not
  need a plan gate.
- Never ask the user to reveal passwords, API keys, tokens, or other secrets.
  Ask for non-secret configuration facts or a secure way to reference them.
