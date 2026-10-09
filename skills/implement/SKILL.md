---
name: implement
description: Delivers a change in thin, independently-verified vertical slices instead of one large pass, anchored to the active agent-issues issue. Use for broad refactors, config or infrastructure changes, multi-file migrations, or other work with no fast test seam. After the last slice, prune duplicate driving tests and keep one public-interface contract per behavior.
argument-hint: Issue ID to implement (or the briefing prepare just reported)
---

This file is the loader for the `implement` skill.

Before you use this skill, call the agent-issues MCP tool `instruction_retrieve` with these arguments:

```json
{
  "key": "skill/implement"
}
```

The first text block contains JSON metadata. The second contains one Markdown part.
If `nextOffset` is not null, call `instruction_retrieve` again with the same `key` and `documentHash`, with `nextOffset` as `offset`. Copy the returned offset; do not calculate it. Continue until `nextOffset` is null. Read all Markdown parts in order before you use this skill. All parts must have the same `documentHash` and `version`.

Follow the complete returned document as this skill's instructions. Required fragments are already included. Do not read separate fragment files. Do not use shell commands or local files to retrieve these instructions.

If the document changes, discard all parts and restart with `key` only. If the tool is unavailable or another retrieval failure occurs, stop and report the failure. Do not continue the task. Do not use cached, bundled, or older-default instructions as a fallback.
