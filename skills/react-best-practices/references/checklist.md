# React Best Practices Checklist

Source basis: Vercel Labs `agent-skills/skills/react-best-practices` (MIT), adapted compactly for Toss Place style Vite React assignment workflows.

## 1. Eliminate Async Waterfalls

- Independent async calls should run in parallel.
- Branch checks should happen before expensive requests when possible.
- Client `useEffect` fetch chains should not cascade when a single query or parallel queries would be simpler.
- Duplicate requests for the same resource should share query keys or a single loader.

## 2. Reduce Bundle Size

- Dynamically import rare modals, charts, maps, editors, or admin-only panels.
- Avoid adding libraries for small native operations.
- Remove dead imports and unused dependencies.
- Keep shared UI primitives small and obvious.

## 3. Improve Client-Side Data Fetching

- Query keys should be centralized and stable.
- Pure API functions should be reusable from query hooks and event handlers.
- Query option factories should be reusable by hooks, prefetch, and invalidation.
- Hooks should define `enabled`, `staleTime`, retry, select, placeholder data, and invalidation deliberately.
- Loading, error, empty, disabled, and pending states should be explicit.

## 4. Improve Abstraction Boundaries

- Page/View components should not parse raw API envelopes.
- Page/View components should not decide raw API key/env error behavior when an adapter can expose screen state.
- Avoid generic `Resource<T>`, `Result<T>`, `{ data, error }`, or vague `current` fields unless they reduce understanding cost.
- Prefer explicit domain names such as `currentWeather`, `forecastDays`, or `orderSubmitErrorMessage`.
- Use view models when raw API data and UI state do not match.

## 5. Reduce Re-Renders

- Move state down when only a subsection needs it.
- Keep input state away from expensive list rendering.
- Split broad contexts by update frequency.
- Avoid unstable object/function props across deep trees.
- Prefer derived values over duplicated state.
- Use `React.memo`, `useMemo`, and `useCallback` only when boundaries and props make them meaningful.

## 6. Improve Rendering Performance

- Virtualize long lists or tables when they are realistically large.
- Avoid expensive synchronous work in render paths.
- Defer non-urgent rendering updates.
- Use transitions for interactions where immediate visual response matters.

## 7. Apply Low-Level JavaScript Optimizations Last

- Avoid repeated parse/format/transform work in hot paths.
- Consolidate repeated array traversals only when the code is a proven hotspot.
- Prefer clear domain code over clever micro-optimizations in assignment code.

## Prioritization Rule

If async waterfalls, duplicate requests, oversized bundles, broad state ownership, or unclear abstraction boundaries exist, fix those before memoization or low-level JavaScript tuning.
