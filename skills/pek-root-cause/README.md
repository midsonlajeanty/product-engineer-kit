# PEK Root Cause

`pek-root-cause` investigates a failure and produces an evidence-based diagnosis with a concrete fix plan. It uses the conversation and files accessible to your agent.

## Install and invoke

In Claude Code, install the whole kit as a plugin:

```text
/plugin install pek --marketplace codeursenior/product-engineer-kit
```

Then invoke it, for example:

```text
/pek:pek-root-cause Explain why this test fails and propose a fix plan.
```

With another agent, install the skill with the [skills CLI](https://github.com/vercel-labs/skills), setting `-a` to your agent (`codex`, `github-copilot`, `cursor`, `claude-code`):

```bash
npx skills add codeursenior/product-engineer-kit --skill pek-root-cause -g -a codex
```

`-g` installs for your user account. Omit it to install for the current project. Start a new session after installation and invoke it with `$pek-root-cause` in Codex or your agent's own mechanism.

Codex keeps it explicit-only through `agents/openai.yaml`: it is not selected automatically there. The skill has no runtime, API key, or dependency on Agent Visualizer or another skill. The workflow is portable Markdown; agents other than Codex have not been behaviorally verified for this skill.

## Scope and limits

The skill produces an analysis and plan. It does not implement or deploy a fix unless separately requested. Missing evidence leads to hypotheses and a next diagnostic step, not a fabricated root cause. One plan is the default; alternatives appear only for meaningful trade-offs.

The [bundled diagnostic loop](references/diagnosing-bugs.md) covers reproduction, falsifiable hypotheses, targeted probes, regression verification, and cleanup. No separate `diagnosing-bugs` skill is needed. Reproduction depends on access to the affected environment and the project's tools; the skill cannot prove a cause from an inaccessible system.

Commits follow the current project's rules. Pushing, publishing, or changing unrelated agent settings requires separate authorization.

## Updates and distribution

```bash
npx skills update pek-root-cause -g
```

Start a new session after updating. If installed files remain stale, reinstall using the install command with `-y` and inspect the installed `SKILL.md`.

GitHub is the source of the installable files after the public mirror synchronizes. The [skills.sh directory](https://skills.sh/docs) uses CLI installation telemetry for discovery, so indexing may lag behind GitHub availability. There is no separate upload step. See [skill provenance](https://github.com/codeursenior/product-engineer-kit/blob/main/docs/skill-provenance.md) for redistribution details.
