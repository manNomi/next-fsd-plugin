---
name: react-best-practices
description: Review, refactor, or plan React code using impact-ordered best practices for Vite React assignments, including async waterfalls, bundle size, client data fetching, React Query usage, re-render risks, rendering performance, and reviewer-readable code.
---

# React Best Practices

Use this when reviewing or improving React performance, architecture, or rendering quality in a Vite React frontend assignment.

This is a compact Toss Place assignment-oriented adaptation of Vercel Labs `agent-skills/skills/react-best-practices` (MIT). For the detailed checklist, read `references/checklist.md` when doing a real review.

## Priority order

Apply improvements in impact order:

1. Eliminate async waterfalls and duplicate requests.
2. Reduce shipped JavaScript and bundle size.
3. Improve client-side data fetching and React Query usage.
4. Reduce unnecessary re-renders.
5. Improve expensive rendering paths.
6. Improve abstraction boundaries and naming clarity.
7. Apply advanced React patterns only for proven hotspots.
8. Apply low-level JavaScript optimizations last.

Do not start with `useMemo`, `useCallback`, or `React.memo` while waterfalls, duplicated requests, broad state ownership, oversized bundles, or unclear data boundaries remain unresolved.

## Workflow

### 1. Establish evidence

Identify:

- slow route or interaction
- user-visible symptom
- expensive component tree, list, or interaction
- bundle risk
- waterfall or duplicated request risk
- current React Query and API-layer strategy
- vague naming or generic wrappers that obscure data flow

If exact metrics are unavailable, inspect code structure and mark findings as inferred.

### 2. Remove async waterfalls first

Check for:

- independent async calls running sequentially
- branch checks performed after expensive requests
- cascading `useEffect` fetches
- duplicated requests for the same resource
- repeated mapper or formatter work in render paths

Prefer:

- `Promise.all` for independent work
- branch-first control flow
- React Query with stable query keys when server state is shared
- one query key per domain resource
- pure mappers outside render when transformations are non-trivial

### 3. Shrink shipped JavaScript

Check for:

- heavy packages imported into always-loaded routes
- optional panels, modals, charts, maps, or editors bundled up front
- utility libraries used for small native operations
- dead imports and unused dependencies

Prefer:

- dynamic import for low-frequency UI
- removing unnecessary dependencies
- keeping shared UI small and explicit

### 4. Improve client data architecture

Check:

- query keys are centralized and stable
- pure API functions are separated from React Query hooks
- hooks define `enabled`, `staleTime`, retry, select, placeholder data, mutation, and invalidation deliberately
- loading, error, empty, disabled, and pending states are explicit
- Page/View components do not interpret raw API envelopes, raw errors, or toast payloads
- adapters or view models expose domain-specific screen state when needed

### 5. Optimize re-renders after boundaries are correct

Check for:

- input state re-rendering large lists
- broad context updates causing tree-wide renders
- unstable objects/functions passed deeply
- expensive derived values recalculated during frequent renders
- `React.memo` used without stable props or a meaningful boundary

Prefer:

- moving state down
- splitting frequently changing state from expensive rendering
- deriving values instead of duplicating state
- memoizing only after component boundaries and props are stable

### 6. Optimize rendering path and low-level code last

Use only when a hotspot remains:

- virtualize large tables/lists
- defer non-urgent updates
- use transitions for non-critical rendering
- reduce repeated parse/transform work
- consolidate repeated array traversals in measured hotspots

## Output format

### 1. Highest-impact findings

List findings in priority order. Use severity: Critical, Important, Minor.

### 2. Evidence

Cite files, routes, components, request flows, bundle risks, naming smells, or clear inferences.

### 3. Recommended fixes

Give an ordered patch plan that starts with waterfalls, bundle/data strategy, state boundaries, then re-render work.

### 4. What not to optimize yet

List memoization, virtualization, generic abstractions, or low-level JS work that should wait until higher-impact issues are handled.

### 5. Verification

List build, typecheck, lint, tests, browser/manual checks, bundle checks, and interaction checks.

### 6. Residual risk

Report remaining uncertainty. Do not claim performance is solved without evidence.
