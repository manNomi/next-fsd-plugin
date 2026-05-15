# Next FSD Plugin

Codex-only marketplace repository for frontend assignment workflow plugins.

## Included Plugin

- `toss-place-fe-superpowers`: a Codex skill pack and subagent orchestration workflow for Toss Place style frontend take-home assignments.

## Install in Codex

Codex currently reads this marketplace from a local filesystem path. Clone the GitHub repository first:

```bash
git clone https://github.com/manNomi/next-fsd-plugin.git
cd next-fsd-plugin
```

Then add this marketplace to `~/.codex/config.toml`. Replace the `source` value with the absolute path where you cloned this repository:

```toml
[marketplaces.next-fsd-plugin]
source_type = "local"
source = "/Users/your-name/path/to/next-fsd-plugin"

[plugins."toss-place-fe-superpowers@next-fsd-plugin"]
enabled = true
```

Restart Codex completely, then start a new session. The plugin should appear as `Toss Place FE Superpowers`.

To update the plugin later:

```bash
cd /Users/your-name/path/to/next-fsd-plugin
git pull
```

Then restart Codex again.

## Verify Installation

In a new Codex session, try:

```text
$toss-place-fe-superpowers:assignment-forensics
```

If Codex says `$assignment-forensics` is not installed, use the namespaced marketplace skill name instead:

```text
$toss-place-fe-superpowers:assignment-forensics
```

Marketplace plugin skills are exposed with the plugin namespace.

## Skill Usage

Use the plugin skills with the marketplace namespace:

```text
$toss-place-fe-superpowers:assignment-forensics
$toss-place-fe-superpowers:timeboxed-assignment-operator
$toss-place-fe-superpowers:stepwise-assignment-runner
$toss-place-fe-superpowers:commerce-order-flow-auditor
$toss-place-fe-superpowers:product-assignment-strategist
$toss-place-fe-superpowers:stack-setup-planner
$toss-place-fe-superpowers:next-rsc-architect
$toss-place-fe-superpowers:simple-fsd-architect
$toss-place-fe-superpowers:api-layer-designer
$toss-place-fe-superpowers:component-boundary-planner
$toss-place-fe-superpowers:reliability-first-planner
$toss-place-fe-superpowers:planning-feedback-loop
$toss-place-fe-superpowers:react-best-practices
$toss-place-fe-superpowers:test-quality-reviewer
$toss-place-fe-superpowers:readme-rationale-writer
$toss-place-fe-superpowers:parallel-assignment-runner
$toss-place-fe-superpowers:review-fix-loop
$toss-place-fe-superpowers:toss-fe-code-review
$toss-place-fe-superpowers:offline-edge-case-checker
$toss-place-fe-superpowers:final-submit-polisher
$toss-place-fe-superpowers:commit-push-pr-agent
```

For an end-to-end orchestrated assignment run:

```text
$toss-place-fe-superpowers:parallel-assignment-runner
Use parallel-assignment-runner to complete this frontend assignment with parallel agents, review-fix loops, verification, and final submission polish.
```

For a planning-first feedback loop before implementation:

```text
$toss-place-fe-superpowers:planning-feedback-loop
이 프론트엔드 과제 구현 전에 목표, 범위, 설계 방향, 리스크, 검증 방법을 피드백 루프로 정리해줘.
```

For product-focused assignment strategy:

```text
$toss-place-fe-superpowers:product-assignment-strategist
이 제품 중심 프론트엔드 과제를 기존 코드베이스 적응, 가정, 트레이드오프, README 제출 전략까지 포함해서 분석해줘.
```

For a 24-hour commerce/order assignment:

```text
$toss-place-fe-superpowers:timeboxed-assignment-operator
Run this assignment around deadline, feature branch, trusted tests, ignored E2E, PR timing, and no-commit-after-submit freeze.
```

```text
$toss-place-fe-superpowers:stepwise-assignment-runner
문항별로 하나씩 요구사항과 선택지를 정리하고, 내 확인을 받은 뒤 구현/검증/다음 문항으로 진행해줘.
```

```text
$toss-place-fe-superpowers:commerce-order-flow-auditor
Audit menu, option selection, cart grouping, pricing, order payload, duplicate submit, Toast errors, and completion flow.
```

For a React/Next.js performance review:

```text
$toss-place-fe-superpowers:react-best-practices
Review this Next.js assignment with react-best-practices and prioritize waterfalls, bundle size, RSC boundaries, cache strategy, and re-render risks.
```

For test quality review:

```text
$toss-place-fe-superpowers:test-quality-reviewer
Review these tests for low-value copy checks, bug-locking expectations, missing regression coverage, pure logic coverage, and accessibility states.
```

For README rationale writing:

```text
$toss-place-fe-superpowers:readme-rationale-writer
Draft README rationale sections for Design Rationale, API / Cache Strategy, React Query Trade-off, FSD Boundary, Error Handling Strategy, Test Strategy, Known Limitations, and Verification Evidence.
```

For verified git delivery:

```text
$toss-place-fe-superpowers:commit-push-pr-agent
Use commit-push-pr-agent to create feature-sized commits, push the branch, and open a PR after verification.
```

For upstream or third-party PR safety:

```text
$toss-place-fe-superpowers:commit-push-pr-agent
Before opening this upstream PR, read the PR template, search existing PRs/issues, verify the problem is real, confirm the change belongs in core, and show me the complete diff and PR body.
```

See `plugins/toss-place-fe-superpowers/README.md` for the full workflow.
