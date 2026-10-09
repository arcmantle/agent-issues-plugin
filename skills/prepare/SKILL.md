---
name: prepare
description: Given whatever the user provides — an ID, a topic, a description, a rough pointer — find all the surrounding tracker context and codebase context relevant to it, then stop for a conversation fork. Widens a single issue, story, or ADR out to its whole owning initiative instead of reporting on just that one entity. Does not narrow to one issue, change any status, or name what to do next. Use at the start of a work session to gather what forked conversations need without growing the session that will run them.
argument-hint: An ID, a topic, or a description of what to look into
---

This file is the loader for the `prepare` skill.

Before you use this skill, call the agent-issues MCP tool `instruction_retrieve` with these arguments:

```json
{
  "key": "skill/prepare"
}
```

The first text block contains JSON metadata. The second contains one Markdown part.
If `nextOffset` is not null, call `instruction_retrieve` again with the same `key` and `documentHash`, with `nextOffset` as `offset`. Copy the returned offset; do not calculate it. Continue until `nextOffset` is null. Read all Markdown parts in order before you use this skill. All parts must have the same `documentHash` and `version`.

Follow the complete returned document as this skill's instructions. Required fragments are already included. Do not read separate fragment files. Do not use shell commands or local files to retrieve these instructions.

If the document changes, discard all parts and restart with `key` only. If the tool is unavailable or another retrieval failure occurs, stop and report the failure. Do not continue the task. Do not use cached, bundled, or older-default instructions as a fallback.
