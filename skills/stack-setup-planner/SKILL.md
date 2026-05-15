---
name: stack-setup-planner
description: Choose the simplest suitable Vite React frontend stack for an assignment, including TypeScript, Tailwind, Emotion, React Query, Vitest, Jest, PNPM, and Yarn Berry.
---

# Stack Setup Planner

Choose the smallest stack that satisfies the assignment and helps reviewers see good frontend judgment. Do not add dependencies to signal seniority.

## Default stack

Prefer Vite + React + TypeScript when:

- the assignment is a client-side app
- the provided project already uses Vite
- fast setup and simple build are important
- routing can be handled by the existing router or a small client router
- the product resembles POS, kiosk, dashboard, order flow, or internal tool UI

Do not replace the provided stack unless the assignment requires it or the existing setup blocks implementation.

## Styling

Prefer the existing styling system first.

Prefer Tailwind when:

- speed of implementation matters
- visual system is simple
- styling requirements are not complex
- the assignment already uses Tailwind

Prefer Emotion when:

- the assignment asks for CSS-in-JS
- component-level dynamic styling is central
- the provided template already uses Emotion

## React Query

Use React Query when:

- API fetching is meaningful
- client-side refetch, mutation, invalidation, optimistic update, caching, loading/error states matter
- multiple components need the same server state
- server state is separate from UI state

Do not use React Query when:

- data is fully static
- data is local mock only
- the existing project uses a simpler clear pattern
- it adds more complexity than value

If React Query is available but not used, document the trade-off in README.

## Testing

- Prefer Vitest for Vite projects.
- Prefer Jest if the project already uses Jest.
- Add tests where they improve confidence: domain logic, validation, mappers, adapters, view models, and critical user flows.

## Output format

### 1. Recommended stack

Name the stack and package manager. Include framework, language, styling, data fetching, and testing.

### 2. Why this stack fits

Tie the choice to assignment requirements and Toss Place style constraints.

### 3. What not to add

List dependencies or frameworks that would add avoidable complexity.

### 4. Initial folder structure

Show the starting structure only. Avoid architecture-only empty folders.

### 5. Setup commands

Provide exact install/scaffold commands only when setup is needed. Prefer the provided project commands when a template exists.

### 6. Required scripts

List expected `dev`, `build`, `lint`, `typecheck`, and `test` scripts when applicable.

### 7. Verification commands

List commands to prove the setup works.

### 8. Risks and trade-offs

State what this stack makes easier and what it does not solve.
