---
description: Open Agent Visualizer to explore this project's agent context, skills and MCP servers
argument-hint: "[folder] [--project-only]"
allowed-tools: Bash(npx -y @codeursenior/pek@latest audit agent:*)
---

Run `npx -y @codeursenior/pek@latest audit agent $ARGUMENTS --no-open` in the background so the session stays free.

Wait for the line that starts with `http://127.0.0.1`, then give the user that full URL, including the `#token=` part. The page shows nothing without the token.

Tell the user the server keeps running until they ask you to stop it.
