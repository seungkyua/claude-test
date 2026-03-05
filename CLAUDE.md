# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains `my-first-plugin`, a starter Claude Code plugin for learning plugin development basics.

## Plugin Structure

Claude Code plugins follow this layout:

```
my-first-plugin/
├── .claude-plugin/
│   └── plugin.json       # Plugin metadata (name, version, author)
├── commands/
│   └── hello.md          # Slash command definitions (/hello)
└── skills/
    └── hello/
        └── SKILL.md      # Skill definitions (invoked via Skill tool)
```

### Key File Formats

**`plugin.json`** — declares plugin identity:
```json
{ "name", "description", "version", "author" }
```

**`commands/*.md`** — define slash commands. Frontmatter supports `description`. The body is the prompt template; use `$ARGUMENTS` to reference arguments passed by the user.

**`skills/<name>/SKILL.md`** — define skills invoked by the Skill tool. Frontmatter supports `description` and `disable-model-invocation: true` (returns the skill prompt directly without an extra model call).
