---
name: toss-fe-code-review
description: Review frontend code like a Toss Place frontend reviewer, prioritizing correctness, reliability, maintainability, state boundaries, abstraction boundaries, naming clarity, API layer design, and edge cases.
---

# Toss FE Code Review

Use this before submission or after implementing a meaningful slice. Prioritize risks over praise. Focus on what could fail in a Toss Place style frontend assignment.

## Review categories

- requirement completeness
- correctness
- reliability
- state ownership
- re-render risk
- React Query usage
- API layer separation
- FSD `entities/` vs `shared/` boundary
- separation of concerns
- abstraction cost
- naming clarity
- view model need
- TypeScript safety
- component responsibility
- UX states
- test quality
- accessibility
- unnecessary dependencies
- README explanation
- commerce order flow correctness
- assignment submission rules

## Severity

- Critical: must fix before submission because it can break core requirements, payment/order-like reliability, or build/runtime correctness.
- Important: should fix because it weakens maintainability, architecture, state correctness, reviewer confidence, or ability to verify behavior.
- Minor: polish that improves clarity but does not block submission.

## Review rules

- Do not lead with general praise.
- Cite concrete files, components, flows, or code patterns when possible.
- Separate requirement gaps from implementation quality.
- Check README and verification, not only code.
- Recommend a patch plan that fixes the highest-risk items first.
- Build a requirement conflict table when the prompt, README, API docs, or implementation imply different interpretations.

## Smell checklists

FSD boundary smell:

- A page or view component imports API response types directly from an API module.
- Generic errors, config, formatters, shared types, UI, or common mappers live in `entities/`.
- Route setup, page composition, widget logic, and entity logic are mixed in one file.

Separation of concerns smell:

- Page/View handles raw API result envelopes.
- Page/View knows API key/env availability details.
- Page/View interprets raw API errors that should be mapped earlier.
- Page/View constructs toast payloads from loader internals.
- Page/View contains business-rule normalization better suited for mapper/adapter code.
- Ask: "Does this component need to know this error exists?"

Over-abstraction smell:

- `{ data, error }`, `Resource<T>`, `Result<T>`, or `AsyncState<T>` hide product meaning.
- A generic wrapper exists for only one or two resources.
- Generic names make reviewers inspect multiple files to understand a simple screen.
- Ask: "Does this abstraction reduce code and understanding cost?"

Naming smell:

- Vague names such as `current`, `data`, `result`, `resource`, `item`, or `state`.
- Ambiguous error names such as `currentErrorMessage` and `forecastErrorMessage` without clear section meaning.
- Prefer names like `currentWeather`, `forecastDays`, `currentWeatherErrorMessage`, `weatherSectionErrors`, or `orderSubmitErrorMessage`.

Test quality smell:

- Tests only check static copy, headings, or shallow rendering.
- Tests lock in current broken output as expected behavior.
- Tests assert implementation details instead of user-visible state transitions.
- Page tests inspect raw toast payload JSON, internal error IDs, or loader internals.
- Page tests ignore loading, error, empty, disabled, retry, pending, and accessibility states.
- Pure logic such as mappers, grouping, formatters, validation, adapters, and partial failure loaders lacks regression coverage.

Commerce order flow smell:

- Option display order differs from the API without a documented reason.
- Required option validation is missing or only enforced after building an invalid payload.
- Cart grouping ignores selected options or treats the same option set as different due to unstable ordering.
- Total count or total price differs between menu CTA, cart CTA, payload, and completion view.
- Submit can run twice because pending/disabled state is missing.
- API 400/404 or network failure is swallowed without user-visible feedback.
- Tests marked as ignored by the assignment are used as blocking verification.

## Output format

### 1. Requirement conflict table

List requirement, possible conflict, chosen interpretation, risk, and README note.

### 2. Critical issues

List Critical issues with why they matter and how to fix them.

### 3. Important improvements

List Important improvements that should be handled before submission when time allows.

### 4. Nice-to-have polish

List Minor polish items.

### 5. State and re-render review

Review state ownership, derived state, expensive renders, input/list separation, unstable props, and memoization.

### 6. API / FSD boundary review

Review pure API functions, React Query hooks, query keys, types, mappers, error handling, and reuse.
Confirm `entities/` contains only domain API-adjacent code. Flag common utilities, common fetchers, common query wrappers, generic mappers, shared UI, global constants, and API response type leakage into page/view components as Important.

### 7. Abstraction / naming / view model review

Review separation of concerns, generic wrapper cost, vague names, raw error leakage, and whether a screen-specific view model would make the code easier to review.

### 8. Test quality review

Review low-value tests, bug-locking tests, implementation-detail tests, missing regression coverage, pure logic coverage, state transition coverage, and accessibility state assertions.

### 9. Edge case review

Review loading, error, empty, disabled, pending, duplicate action, network failure, stale data, and invalid data behavior.

### 10. Commerce order flow review

Review catalog/menu filtering, item detail loading, option rule matrix, cart grouping, price calculation, order payload, duplicate submit prevention, order completion lookup, and Toast/error behavior.

### 11. README / submission review

Review install/dev/build/test instructions, ignored-test rationale, feature branch/PR requirements, no-commit-after-submit rule, Design Rationale, API/Data Strategy, React Query Trade-off, FSD Boundary, Error Handling Strategy, Test Strategy, limitations, and verification evidence.

### 12. Recommended patch plan

Provide an ordered patch plan that starts with Critical issues, then Important improvements, then polish.
Group recommended fixes into feature-sized commit candidates when useful.
