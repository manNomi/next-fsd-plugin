---
name: vite-react-architect
description: Design a Vite React TypeScript assignment architecture with route setup, Simple FSD layers, pure API functions, React Query usage, client cache policy, state placement, component boundaries, and verification.
---

# Vite React Architect

Use this when the assignment is likely a Vite + React + TypeScript project or when the provided project is a client-side React app.

## Core principle

Prefer the simplest client-side architecture that makes requirements, data flow, state ownership, and reviewer intent obvious.

## Decision checklist

1. What routes or screens exist?
2. Which screens are already implemented, partially implemented, or TODO-only?
3. Which data comes from API, mock API, fixture, or local state?
4. Which data should be loaded with React Query?
5. Which data is static enough for a simple constant or fixture import?
6. Which actions need mutation, invalidation, retry, pending state, or duplicate-submit prevention?
7. Which state is server state, local UI state, form state, derived state, or persisted state?
8. Where should state live so only the relevant UI re-renders?
9. Which API functions, query keys, hooks, mappers, and view models are needed?
10. Which abstractions would make the code harder to read than explicit domain names?

## React Query usage

Use React Query when:

- API fetching is meaningful and shared across screens or widgets
- loading/error/retry states should be modeled consistently
- mutations need pending state, invalidation, optimistic updates, or retry behavior
- user input changes the query
- multiple components need the same server state without prop drilling

Do not use React Query when:

- data is static or local-only
- the project already has a simpler established pattern
- one direct effect or loader would be clearer for the assignment
- it adds more code than it removes

If React Query is not used despite being available, document why in README.

## Client cache routine

- Define stable query keys in the domain API module.
- Choose `staleTime` based on user-visible freshness, not habit.
- Use invalidation after mutations that change visible server state.
- Avoid long-lived cache for order/payment-like progress that must reflect the latest user action.
- Prefer explicit retry behavior for transient failures and clear error UI for non-recoverable failures.
- Keep server state separate from local UI state.

## Simple FSD shape

```text
src/
  app/
    providers/
    router/
    styles/
  views/
    menu/
    detail/
    cart/
  widgets/
  entities/
  shared/
```

`app/` owns app bootstrapping, providers, router setup, and global styles. Real screen composition belongs in `views/` or the existing project page layer.

`entities/` contains only domain API-adjacent code: pure API functions, query hooks, query keys/options, API-bound types, and API response mappers.

Common clients, formatters, config, constants, UI primitives, and generic helpers belong in `shared/`.

## Output format

### 1. App architecture

Describe router setup, providers, global styles, and where screen composition lives.

### 2. Screen inventory

List screens/routes, current implementation status, and primary user flow.

### 3. Data flow

Map API/mock/fixture/local data to pure API functions, query hooks, mappers, and view models.

### 4. React Query plan

State which queries and mutations are needed, query keys, staleTime, retry, enabled conditions, invalidation, and when React Query is intentionally not used.

### 5. State placement

Map server state, local UI state, form state, pending state, error state, and derived state to owners.

### 6. Component boundaries

List view, widget, and shared UI boundaries based on state ownership, re-render risk, and reviewer readability.

### 7. FSD structure

Show the smallest useful folder structure and what should stay page-local.

### 8. Abstractions to avoid

List generic wrappers, reusable layers, or clever patterns that are not justified yet.

### 9. Verification

List build, lint, typecheck, tests, browser/manual checks, and screenshot/design comparison when relevant.

### 10. README notes

List architecture, React Query, FSD, state, error handling, and trade-off notes to document.
