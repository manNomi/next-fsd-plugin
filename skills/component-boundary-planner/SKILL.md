---
name: component-boundary-planner
description: Plan React component boundaries based on state ownership, re-render minimization, domain responsibility, view-model boundaries, naming clarity, and assignment maintainability.
---

# Component Boundary Planner

Split components to minimize the rendering impact of state changes. A component boundary should communicate ownership, responsibility, or rendering isolation.

## Rules

- Do not split only because JSX is long.
- Do not keep all state in the page by default.
- Keep state close to where it is used.
- Move state down when only a subsection needs it.
- Separate frequently changing state from expensive rendering.
- Avoid input state re-rendering large lists.
- Prefer derived values over duplicated state.
- Avoid passing unstable objects/functions deeply.
- Use `React.memo` only when there is a clear boundary and stable props.
- Do not make Page/View components interpret raw API errors, env/API key state, or toast payload internals.
- Use explicit domain names instead of vague `data`, `result`, `current`, or `resource` props.

## Create a separate component when

- it owns frequently changing state
- it renders an expensive list
- it has a distinct interaction flow
- it represents a meaningful domain section
- it has independent loading/error/empty state
- it prevents unrelated UI from re-rendering
- it improves page composition

## Keep code together when

- splitting creates artificial props
- there is no independent state or behavior
- the component would have a vague name
- the split makes data flow harder
- it is one-off static markup

## Output format

### 1. State inventory

List server state, local UI state, form/input state, derived state, pending state, and error state.

### 2. State owner map

Map each state item to the smallest component that should own it.

### 3. View-model boundary

State whether Page/View should receive explicit screen state instead of raw API, env, or error objects.

### 4. Re-render risk map

Identify frequent updates, expensive lists, broad parent renders, and unstable props.

### 5. Component tree

Show the proposed tree and each component's responsibility.

### 6. Props flow

List important props and avoid passing entire objects when smaller values are enough.

### 7. What should be derived

List values that should be computed from existing state instead of stored separately.

### 8. What should be split

List components to extract and the exact reason for each boundary.

### 9. What should stay together

List markup or logic that should remain local for readability.

### 10. Final recommendation

Summarize the boundaries to implement first and memoization to avoid unless proven necessary.
