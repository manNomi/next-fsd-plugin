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
- React/Next.js performance best-practice review
- reliability review
- review-fix loops
- planning feedback loops
- optional parallel subagent orchestration
- final submission polish

## When to use

Use this plugin when:

- starting a frontend assignment
- deciding between Vite and Next.js
- designing Next.js RSC architecture
- deciding static rendering, ISR, revalidation, and `no-store` boundaries
- designing API and React Query layers
- splitting components
- reviewing React/Next.js performance risks
- reviewing code before submission
- planning a non-trivial implementation before coding
- running an end-to-end assignment workflow with explicitly requested parallel agents
- repeating review, fix, and verification loops after implementation

## Skill workflow

### Manual skill workflow

Use this when you want to control each step yourself:

1. `$toss-place-fe-superpowers:planning-feedback-loop`
2. `$toss-place-fe-superpowers:assignment-forensics`
3. `$toss-place-fe-superpowers:stack-setup-planner`
4. `$toss-place-fe-superpowers:next-rsc-architect`
5. `$toss-place-fe-superpowers:simple-fsd-architect`
6. `$toss-place-fe-superpowers:api-layer-designer`
7. `$toss-place-fe-superpowers:component-boundary-planner`
8. `$toss-place-fe-superpowers:reliability-first-planner`
9. `$toss-place-fe-superpowers:react-best-practices`
10. `$toss-place-fe-superpowers:toss-fe-code-review`
11. `$toss-place-fe-superpowers:offline-edge-case-checker`
12. `$toss-place-fe-superpowers:final-submit-polisher`

When this plugin is installed through a Codex marketplace, use the namespaced skill names above.

### Planning-first workflow

Use this before implementation when the task is non-trivial and you want to refine the direction with feedback:

1. `$toss-place-fe-superpowers:planning-feedback-loop`
2. Confirm or revise the plan.
3. Continue with the manual workflow or the end-to-end orchestrator workflow.

The planning feedback loop restates the goal, drafts a plan, asks for focused feedback, revises the plan, reviews risk and validation, and only then finalizes an executable plan.

### End-to-end orchestrator workflow

Use this when you explicitly want Codex to coordinate multiple agents, parallel work slices, review-fix loops, verification, and final polish:

1. `$toss-place-fe-superpowers:parallel-assignment-runner`
2. `$toss-place-fe-superpowers:review-fix-loop`
3. `$toss-place-fe-superpowers:final-submit-polisher`

The parallel runner uses Codex subagents only when you explicitly ask for parallel agents, multiple agents, an agent team, delegated work, or a review loop. It keeps the main thread responsible for critical-path decisions, integration, verification, and final reporting.

## Example prompts

### `$toss-place-fe-superpowers:planning-feedback-loop`

```text
$toss-place-fe-superpowers:planning-feedback-loop
이 프론트엔드 과제 구현 전에 목표, 범위, 설계 방향, 리스크, 검증 방법을 피드백 루프로 정리해줘.
```

```text
$toss-place-fe-superpowers:planning-feedback-loop
Before implementation, help me refine the goal, scope, architecture direction, risks, and validation plan through a feedback loop.
```

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

```text
$toss-place-fe-superpowers:next-rsc-architect
Plan cache-efficient Next.js architecture using static rendering, ISR, tag/path revalidation, no-store only where necessary, and React Query hydration where useful.
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

### `$toss-place-fe-superpowers:react-best-practices`

```text
$toss-place-fe-superpowers:react-best-practices
Review this Next.js assignment with react-best-practices and prioritize waterfalls, bundle size, RSC boundaries, cache strategy, and re-render risks.
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
- Keep `app/` as folder routing and delegate real page composition to `views/`.
- Keep state as low as possible.
- Cache what can be cached.
- Prefer static rendering, `force-cache`, `revalidate`, ISR, and tag/path revalidation for public or periodically changing data.
- Reserve `no-store` for user-specific, permission-specific, payment/order-progress, or always-fresh data.
- Prefer React Query hydration when server-prefetched data should be consumed by client widgets through hooks.
- Align React Query `staleTime` with the Next.js server cache strategy.
- Review React performance in impact order: waterfalls, bundle size, RSC/cache/data fetching, then re-renders.
- Separate pure API functions from React Query hooks.
- Keep query option factories reusable across `prefetchQuery`, hydration, and hooks.
- Use Simple FSD without over-engineering.
- Split component boundaries based on state ownership and re-rendering.
- Plan non-trivial work before implementation and ask for focused feedback.
- Ask for all page screenshots and Figma/design references before large UI implementation.
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
