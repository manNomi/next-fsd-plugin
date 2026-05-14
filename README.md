# Next FSD Plugin

Codex-only marketplace repository for frontend assignment workflow plugins.

## Included Plugin

- `toss-place-fe-superpowers`: a Codex skill pack for Toss Place style frontend take-home assignments.

## Local Codex Setup

Clone this repository, then add the marketplace to `~/.codex/config.toml`:

```toml
[marketplaces.next-fsd-plugin]
source_type = "local"
source = "/absolute/path/to/next-fsd-plugin"

[plugins."toss-place-fe-superpowers@next-fsd-plugin"]
enabled = true
```

Restart Codex and start a new session.

## Skill Usage

Use the plugin skills with the marketplace namespace:

```text
$toss-place-fe-superpowers:assignment-forensics
$toss-place-fe-superpowers:stack-setup-planner
$toss-place-fe-superpowers:next-rsc-architect
$toss-place-fe-superpowers:simple-fsd-architect
$toss-place-fe-superpowers:api-layer-designer
$toss-place-fe-superpowers:component-boundary-planner
$toss-place-fe-superpowers:reliability-first-planner
$toss-place-fe-superpowers:toss-fe-code-review
$toss-place-fe-superpowers:offline-edge-case-checker
$toss-place-fe-superpowers:final-submit-polisher
```

See `plugins/toss-place-fe-superpowers/README.md` for the full workflow.
