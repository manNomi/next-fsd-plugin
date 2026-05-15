---
name: stepwise-assignment-runner
description: Run a frontend take-home assignment question by question or screen by screen, locking requirements, decisions, recommended defaults, implementation scope, verification, and handoff with the user before moving to the next unit.
---

# Stepwise Assignment Runner

Use this as the default execution workflow for non-trivial frontend assignments, especially timeboxed product assignments with multiple screens or numbered requirements. The goal is to avoid implementing everything at once. Work one question or screen at a time with the user.

## Hard gates

- Do not implement all screens or all requirements at once.
- Do not implement all screens at once.
- Before each unit, explain the requirement, decision points, recommended default, and what user confirmation is needed.
- Do not finalize the implementation plan for a unit until the user confirms or says to proceed with the recommended default.
- After each unit, verify the result, report residual risk, and ask before moving to the next unit.
- If time is running out, pause the next-unit plan and revisit the cutline with the user.
- Keep the current unit small enough to review in one conversation turn.
- Do not spawn subagents unless the user explicitly asks for parallel or delegated work.

## Default unit order

Use assignment text first. If no better unit order is provided, default to:

1. Submission and timebox operation
2. Shared API/domain model foundation
3. Menu or list screen
4. Detail and option-selection screen
5. Cart screen
6. Order submit flow
7. Completion or result screen
8. Tests, README, final polish, PR

For non-commerce assignments, map units to the assignment's numbered questions, pages, or user flows.

## Per-unit loop

Repeat this loop for every unit:

1. Restate the current unit's goal.
2. Extract explicit requirements and hidden reviewer risks.
3. List decision points and trade-offs.
4. Recommend a default direction.
5. Ask for focused user confirmation.
6. Implement only the confirmed unit.
7. Run available verification for that unit.
8. Report what changed, what passed, what remains, and the next proposed unit.

## Decision points to lock

For each unit, decide only what matters for that unit:

- source of truth: API, fixture, local state, URL, storage, or server state
- state owner and component boundary
- loading, error, empty, disabled, pending, and retry behavior
- validation and failure feedback
- test target and manual QA target
- README assumption or trade-off to record
- whether the unit is MVP, polish, optional, or cutline-sensitive

## Commerce unit defaults

For commerce/order assignments, use these defaults unless the user or codebase says otherwise:

- Shared foundation: API contracts, pure mappers, option validation, cart grouping, and price calculation before screen wiring.
- Menu/list: category filter and CTA summary are one unit.
- Detail/options: option display order, required defaults, min/max validation, and add-to-cart transition are one unit.
- Cart: grouping key, quantity/remove, total count/price, and empty state are one unit.
- Submit: payload correctness, pending guard, duplicate submit prevention, and API error Toast are one unit.
- Completion: order lookup, not-found fallback, total display, and return transition are one unit.

## Output format

### 1. Assignment map

List all units in order. Mark current, pending, done, cutline, and optional units.

### 2. Current question / screen

Restate the current unit's goal, explicit requirements, and hidden risks.

### 3. Decision points

List the decisions needed before this unit can be implemented.

### 4. Recommended default

Give a concrete default for each decision and explain the trade-off briefly.

### 5. User confirmation needed

Ask focused questions or say exactly what "proceed with recommended defaults" means.

### 6. Implementation plan for this unit

After confirmation, list the exact files or areas to modify and what will not be touched.

### 7. Verification for this unit

List deterministic checks and manual QA specific to this unit.

### 8. Handoff to next unit

After verification, summarize completion, residual risk, README notes, and the next proposed unit.
