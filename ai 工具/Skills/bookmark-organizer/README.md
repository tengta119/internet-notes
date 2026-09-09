# bookmark-organizer Skill

A safety-first Agent Skill for reorganizing Microsoft Edge bookmarks through `chromium-bookmarks-mcp`.

## Intended hosts

Works best with Agent environments that support `SKILL.md`-style skills, including workflows built around Claude Code, Codex, Pi, or similar coding agents.

## Requirements

- Microsoft Edge running
- Chromium Bookmarks MCP connected and responsive
- The Skill installed in the host Agent's skills directory

## Core behavior

The Skill enforces:

`analyze -> propose -> explicit approval -> backup -> dry-run -> apply -> verify`

Destructive operations are never performed silently.

## Files

- `SKILL.md` — main skill definition
- `references/decision-rubric.md` — classification and confidence rubric
- `references/output-template.md` — standardized proposal format
