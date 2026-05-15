# Toss Place FE Superpowers

A standalone Codex plugin for starting a frontend take-home assignment with a focused Vite React workflow.

This repo is intentionally small: clone it before an assignment, enable the plugin in Codex, then use the skills to analyze the prompt, make decisions one screen at a time, implement carefully, review the result, and polish the final submission.

## What This Helps With

- deadline and submission rules
- question-by-question assignment progress
- requirement and hidden evaluation analysis
- product assumptions and trade-offs
- Vite React TypeScript architecture
- Simple FSD without architecture-only folders
- API layer and React Query decisions
- component boundaries and re-render risks
- over-abstraction, naming, and view model review
- reliability and offline-commerce edge cases
- test quality review
- README rationale and final submission polish

## Start An Assignment

1. Clone this repo.
2. Enable this directory as a local Codex plugin.
3. Restart Codex.
4. Start the assignment from the target project directory.
5. Use the stepwise flow below.

## Recommended Flow

Use these skills in order for a typical Toss-style product assignment:

```text
$toss-place-fe-superpowers:timeboxed-assignment-operator
$toss-place-fe-superpowers:stepwise-assignment-runner
$toss-place-fe-superpowers:product-assignment-strategist
$toss-place-fe-superpowers:assignment-forensics
$toss-place-fe-superpowers:stack-setup-planner
$toss-place-fe-superpowers:vite-react-architect
$toss-place-fe-superpowers:simple-fsd-architect
$toss-place-fe-superpowers:api-layer-designer
$toss-place-fe-superpowers:component-boundary-planner
$toss-place-fe-superpowers:abstraction-boundary-reviewer
$toss-place-fe-superpowers:reliability-first-planner
$toss-place-fe-superpowers:toss-fe-code-review
$toss-place-fe-superpowers:test-quality-reviewer
$toss-place-fe-superpowers:offline-edge-case-checker
$toss-place-fe-superpowers:readme-rationale-writer
$toss-place-fe-superpowers:final-submit-polisher
```

For commerce/order-flow assignments, add:

```text
$toss-place-fe-superpowers:commerce-order-flow-auditor
```

For React performance review, add:

```text
$toss-place-fe-superpowers:react-best-practices
```

## Practical Starter Prompts

```text
$toss-place-fe-superpowers:timeboxed-assignment-operator
이 과제의 제한시간, 제출 브랜치, PR 규칙, 제출 후 커밋 금지 조건을 먼저 정리해줘.
```

```text
$toss-place-fe-superpowers:stepwise-assignment-runner
문항별로 하나씩 요구사항과 선택지를 정리하고, 내 확인을 받은 뒤 구현/검증/다음 문항으로 진행해줘.
```

```text
$toss-place-fe-superpowers:vite-react-architect
Vite React TypeScript 기준으로 routing, API layer, React Query, state placement, FSD, verification을 설계해줘.
```

```text
$toss-place-fe-superpowers:abstraction-boundary-reviewer
Page/View가 raw API/error 상태를 너무 많이 알고 있는지, generic abstraction이 과한지 리뷰해줘.
```

```text
$toss-place-fe-superpowers:final-submit-polisher
README, 실행 방법, 검증 커맨드, 구현 범위, trade-off, known limitation, 최종 diff를 제출 전 기준으로 점검해줘.
```

## Core Principles

- Do not implement everything at once.
- Move one question or screen at a time.
- Ask for user confirmation before locking behavior.
- Prefer Vite + React + TypeScript unless the assignment clearly provides another stack.
- Respect the existing project structure and design system.
- Keep `entities/` limited to domain API-adjacent code.
- Put common utilities, fetchers, UI, config, constants, and generic helpers in `shared/`.
- Separate pure API functions from React Query hooks.
- Use React Query only when server state management adds value.
- Prefer explicit domain names and view models over generic wrappers.
- Optimize for reviewer-readable code, not impressive architecture.
- Treat README as part of the submitted product.

## Included Skills

- `timeboxed-assignment-operator`
- `stepwise-assignment-runner`
- `product-assignment-strategist`
- `assignment-forensics`
- `commerce-order-flow-auditor`
- `stack-setup-planner`
- `vite-react-architect`
- `simple-fsd-architect`
- `api-layer-designer`
- `component-boundary-planner`
- `abstraction-boundary-reviewer`
- `reliability-first-planner`
- `react-best-practices`
- `test-quality-reviewer`
- `toss-fe-code-review`
- `offline-edge-case-checker`
- `readme-rationale-writer`
- `final-submit-polisher`

## Limitations

- This plugin does not guarantee passing an assignment.
- It is a workflow guide, not a replacement for engineering judgment.
- It assumes a frontend product assignment, usually close to Vite React.
- Commerce/order-flow checks should be adapted if the assignment domain is different.
