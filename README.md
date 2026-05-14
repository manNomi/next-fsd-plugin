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
$toss-place-fe-superpowers:stack-setup-planner
$toss-place-fe-superpowers:next-rsc-architect
$toss-place-fe-superpowers:simple-fsd-architect
$toss-place-fe-superpowers:api-layer-designer
$toss-place-fe-superpowers:component-boundary-planner
$toss-place-fe-superpowers:reliability-first-planner
$toss-place-fe-superpowers:parallel-assignment-runner
$toss-place-fe-superpowers:review-fix-loop
$toss-place-fe-superpowers:toss-fe-code-review
$toss-place-fe-superpowers:offline-edge-case-checker
$toss-place-fe-superpowers:final-submit-polisher
```

For an end-to-end orchestrated assignment run:

```text
$toss-place-fe-superpowers:parallel-assignment-runner
Use parallel-assignment-runner to complete this frontend assignment with parallel agents, review-fix loops, verification, and final submission polish.
```

See `plugins/toss-place-fe-superpowers/README.md` for the full workflow.
