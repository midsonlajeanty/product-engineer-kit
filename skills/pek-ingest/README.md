# PEK Ingest

`pek-ingest` turns supplied documents and validated decisions into durable, linked project context. It uses the conversation and files accessible to your agent.

## Install and invoke

In Claude Code, install the whole kit as a plugin:

```text
/plugin install pek --marketplace codeursenior/product-engineer-kit
```

Then invoke it, for example:

```text
/pek:pek-ingest Record the durable decisions from this discussion in the project context.
```

With another agent, install the skill with the [skills CLI](https://github.com/vercel-labs/skills), setting `-a` to your agent (`codex`, `github-copilot`, `cursor`, `claude-code`):

```bash
npx skills add codeursenior/product-engineer-kit --skill pek-ingest -g -a codex
```

`-g` installs for your user account. Omit it to install for the current project. Start a new session after installation and invoke it with `$pek-ingest` in Codex or your agent's own mechanism.

The agent can select it automatically when the request matches, or you can invoke it explicitly. The skill has no runtime, API key, or dependency on Agent Visualizer or another skill. The workflow is portable Markdown; agents other than Codex have not been behaviorally verified for this skill.

## Scope and limits

The invocation requests context edits in the current project. The skill searches for existing notes, follows project instructions, preserves source links, and reports contradictions instead of inventing a resolution. Global user context requires an explicit request or workspace instruction. It does not copy a private source into public documentation.

Obsidian handling is included as instructions for preserving properties, links, embeds, and attachments. No Obsidian skill, plugin, or application is required for Markdown edits. Rendering and unavailable linked sources are reported as verification limits. It cannot retain information beyond the files it actually updates.

Commits follow the current project's rules. Pushing, publishing, or changing unrelated agent settings requires separate authorization.

## Updates and distribution

```bash
npx skills update pek-ingest -g
```

Start a new session after updating. If installed files remain stale, reinstall using the install command with `-y` and inspect the installed `SKILL.md`.

GitHub is the source of the installable files after the public mirror synchronizes. The [skills.sh directory](https://skills.sh/docs) uses CLI installation telemetry for discovery, so indexing may lag behind GitHub availability. There is no separate upload step. See [skill provenance](https://github.com/codeursenior/product-engineer-kit/blob/main/docs/skill-provenance.md) for redistribution details.
