---
name: Agent Issues
description: "Use when working from an agent-issues issue, an ISS id, or an issue-guided implementation task. This agent starts by loading issue context with agent-issues, keeps changes scoped to that record, and validates the touched slice before expanding."
argument-hint: "Issue-first task, e.g. ISS53 implement context search badge"
user-invocable: true
---

This file is the loader for the `agent-issues` agent.

Before you use this agent, call the agent-issues MCP tool `instruction_retrieve` with these arguments:

```json
{
  "key": "agent/agent-issues"
}
```

The first text block contains JSON metadata. The second contains one Markdown part.
If `nextOffset` is not null, call `instruction_retrieve` again with the same `key` and `documentHash`, with `nextOffset` as `offset`. Copy the returned offset; do not calculate it. Continue until `nextOffset` is null. Read all Markdown parts in order before you use this agent. All parts must have the same `documentHash` and `version`.

Follow the complete returned document as this agent's instructions. Required fragments are already included. Do not read separate fragment files. Do not use shell commands or local files to retrieve these instructions.

If the document changes, discard all parts and restart with `key` only. If the tool is unavailable or another retrieval failure occurs, stop and report the failure. Do not continue the task. Do not use cached, bundled, or older-default instructions as a fallback.
