# Toss Place FE Superpowers

## What this is

A Codex skill pack for frontend take-home assignments, inspired by Superpowers, customized for Toss Place style frontend work. It can be used skill-by-skill or as a Codex subagent orchestration workflow.

## Why this exists

This plugin prevents jumping directly into code and instead enforces:

- requirement analysis
- stack selection
- Next.js RSC/caching decisions
- Simple FSD architecture
- API layer separation
- re-render-aware component boundaries
- reliability review
- review-fix loops
- optional parallel subagent orchestration
- final submission polish

## When to use

Use this plugin when:

- starting a frontend assignment
- deciding between Vite and Next.js
- designing Next.js RSC architecture
- designing API and React Query layers
- splitting components
- reviewing code before submission
- running an end-to-end assignment workflow with explicitly requested parallel agents
- repeating review, fix, and verification loops after implementation

## Skill workflow

### Manual skill workflow

Use this when you want to control each step yourself:

1. `$toss-place-fe-superpowers:assignment-forensics`
2. `$toss-place-fe-superpowers:stack-setup-planner`
3. `$toss-place-fe-superpowers:next-rsc-architect`
4. `$toss-place-fe-superpowers:simple-fsd-architect`
5. `$toss-place-fe-superpowers:api-layer-designer`
6. `$toss-place-fe-superpowers:component-boundary-planner`
7. `$toss-place-fe-superpowers:reliability-first-planner`
8. `$toss-place-fe-superpowers:toss-fe-code-review`
9. `$toss-place-fe-superpowers:offline-edge-case-checker`
10. `$toss-place-fe-superpowers:final-submit-polisher`

When this plugin is installed through a Codex marketplace, use the namespaced skill names above.

### End-to-end orchestrator workflow

Use this when you explicitly want Codex to coordinate multiple agents, parallel work slices, review-fix loops, verification, and final polish:

1. `$toss-place-fe-superpowers:parallel-assignment-runner`
2. `$toss-place-fe-superpowers:review-fix-loop`
3. `$toss-place-fe-superpowers:final-submit-polisher`

The parallel runner uses Codex subagents only when you explicitly ask for parallel agents, multiple agents, an agent team, delegated work, or a review loop. It keeps the main thread responsible for critical-path decisions, integration, verification, and final reporting.

## Example prompts

### `$toss-place-fe-superpowers:parallel-assignment-runner`

```text
Use parallel-assignment-runner to complete this frontend assignment with parallel agents, review-fix loops, verification, and final submission polish.
```

```text
parallel-assignment-runner로 이 프론트엔드 과제를 병렬 에이전트, 리뷰-수정 루프, 검증, 최종 제출 polish까지 진행해줘.
```

### `$toss-place-fe-superpowers:review-fix-loop`

```text
$toss-place-fe-superpowers:review-fix-loop
Review the current implementation, fix Critical and requirement/correctness/reliability Important findings, and re-run verification up to 3 times.
```

### `$toss-place-fe-superpowers:assignment-forensics`

```text
$toss-place-fe-superpowers:assignment-forensics
Analyze this take-home assignment. Extract the MVP, hidden evaluation points, Toss Place reliability risks, and submission checklist.
```

### `$toss-place-fe-superpowers:stack-setup-planner`

```text
$toss-place-fe-superpowers:stack-setup-planner
Decide whether this assignment should use Vite or Next.js, Tailwind or Emotion, React Query or plain fetch, and which test setup is enough.
```

### `$toss-place-fe-superpowers:next-rsc-architect`

```text
$toss-place-fe-superpowers:next-rsc-architect
For this Next.js App Router assignment, decide what stays server-side, what needs client boundaries, and how caching should work.
```

### `$toss-place-fe-superpowers:simple-fsd-architect`

```text
$toss-place-fe-superpowers:simple-fsd-architect
Design a lightweight folder structure for this assignment without creating architecture-only folders.
```

### `$toss-place-fe-superpowers:api-layer-designer`

```text
$toss-place-fe-superpowers:api-layer-designer
Separate pure API functions, React Query hooks, query keys, types, and mappers for this assignment.
```

### `$toss-place-fe-superpowers:component-boundary-planner`

```text
$toss-place-fe-superpowers:component-boundary-planner
Split components by state ownership, Server/Client boundaries, and re-render risk.
```

### `$toss-place-fe-superpowers:reliability-first-planner`

```text
$toss-place-fe-superpowers:reliability-first-planner
Create an implementation plan that covers loading, error, empty, disabled, pending, retry, and duplicate action prevention.
```

### `$toss-place-fe-superpowers:toss-fe-code-review`

```text
$toss-place-fe-superpowers:toss-fe-code-review
Review this diff and prioritize requirement gaps, reliability risks, state boundaries, API layer issues, and README weaknesses.
```

### `$toss-place-fe-superpowers:offline-edge-case-checker`

```text
$toss-place-fe-superpowers:offline-edge-case-checker
Test this assignment against POS, kiosk, table order, payment/order, slow network, duplicate submit, and stale data scenarios.
```

### `$toss-place-fe-superpowers:final-submit-polisher`

```text
$toss-place-fe-superpowers:final-submit-polisher
Check README, scripts, verification commands, trade-offs, limitations, final diff quality, and final message before submission.
```

## Design principles

- Server Component by default.
- Client Component only when necessary.
- Keep state as low as possible.
- Cache what can be cached.
- Separate pure API functions from React Query hooks.
- Use Simple FSD without over-engineering.
- Split component boundaries based on state ownership and re-rendering.
- Use Codex subagents only when parallel/delegated work is explicitly requested.
- Give each worker a disjoint write scope.
- Run review-fix loops until stop conditions are met or risks are reported.
- Prioritize reliability, maintainability, and clear trade-offs.
- Prefer small, reviewer-readable architecture over impressive abstractions.

## Limitations

- This does not guarantee passing an assignment.
- This is a workflow guide, not a replacement for engineering judgment.
- Adapt every recommendation to the actual assignment requirements.
- The plugin is Codex-first and does not include hooks, MCP servers, assets, or non-Codex platform support.
- This is not a new agent runtime; it is a Codex subagent orchestration workflow.
- Parallel work can increase token and time cost.
- If worker write scopes overlap, the main thread must stop and coordinate before continuing.
