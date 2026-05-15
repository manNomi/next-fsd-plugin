---
name: test-quality-reviewer
description: Review frontend assignment tests for meaningful regression coverage, state transitions, pure logic validation, accessibility states, and low-value or bug-locking test smells.
---

# Test Quality Reviewer

Use this after tests are written or during code review when the assignment includes test files, validation logic, mappers, formatters, API loaders, UI state handling, or accessibility states.

## Core principle

Good tests protect requirements and user-visible state transitions. Low-value tests only prove that text renders. Dangerous tests can lock in the current bug.

If the assignment explicitly says an E2E test or existing test does not reflect the requirements, do not use that test as blocking verification. Mark it as ignored by assignment instruction and document the reason.

## Review priorities

1. Find tests that lock in incorrect behavior.
2. Find missing regression tests for important flows.
3. Prefer pure logic tests for mappers, formatters, grouping, validation, and API loaders.
4. Prefer page/component tests that verify states, roles, disabled behavior, retry behavior, and accessibility signals.
5. Remove or deprioritize tests that only check static copy unless that copy is a requirement.

## Bad test smells

- A test only checks that generic text renders, such as `Welcome to` or a section heading.
- A test asserts implementation details instead of user-visible behavior.
- A test fixes a current bug as expected output, such as a wrong temperature range like `21.40℃ / 24.60℃`.
- A page test checks UI copy but ignores loading, error, empty, disabled, retry, or pending states.
- A test mocks toast payloads or internal callbacks at the wrong level instead of verifying the user outcome.
- A page test asserts raw toast payload JSON, internal error IDs, API key flags, or loader settlement objects instead of visible UI states.
- A test mirrors component structure so closely that refactoring breaks it without a behavior change.

## Good test targets

- API loader partial failure and recovery behavior.
- mapper, adapter, view model, grouping, timezone formatter, validation, sorting, and domain conversion logic.
- Duplicate submit prevention and disabled state during pending actions.
- Error roles, retry buttons, empty states, and invalid data behavior.
- Accessibility states such as `aria-expanded`, disabled controls, alert/error role, and keyboard/touch behavior.
- React Query mutation/invalidation or retry behavior when client server state is meaningful.
- Commerce/order logic: option min/max validation, cart grouping, price calculation, order payload shape, duplicate submit prevention, API error handling, and order completion not-found behavior.

## Output format

### 1. High-value tests

List tests that protect real requirements, state transitions, regressions, accessibility, or pure domain logic.

### 2. Low-value tests

List tests that only verify static text, headings, implementation details, or shallow rendering.

### 3. Bug-locking tests

List tests that appear to encode current broken behavior as expected behavior. Explain the correct behavior to assert instead.

### 4. Missing regression coverage

List missing tests for partial failure, retry, duplicate action prevention, validation, edge cases, accessibility, mapper/adapter/view-model logic, option rules, cart grouping, price calculation, and order payload correctness.

### 5. Recommended test patch plan

Give an ordered plan: mark assignment-ignored tests as non-blocking, delete or rewrite low-value tests, fix bug-locking tests, add high-value regression tests, then run verification.
