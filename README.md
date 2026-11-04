# Auto Memory for skills.sh

A custom skill for persistent project memory that helps an agent remember durable decisions, business context, investigation outcomes, and tricky gotchas without redoing research in every session.

This repository is organized to work with the skills.sh ecosystem: each skill lives under a `skills/` directory and exposes its definition in a `SKILL.md` file.

## What this skill does

The `auto-memory` skill keeps a compact, searchable memory store inside `.claude/memory/` so the next task can quickly recover:

- important business decisions
- trade-offs and their reasoning
- project context not obvious from the code alone
- investigation outcomes and root causes
- recurring failure modes and constraints

The memory is intentionally curated: only durable, non-obvious facts are saved, and stale or invalid entries are updated or removed when they no longer match the current branch.

## Repository structure

```text
.
├── README.md
└── skills/
    └── auto-memory/
        └── SKILL.md
```

This is the standard structure used by skills.sh-compatible repositories:

- the root README explains the project
- `skills/` contains one folder per skill
- each skill folder contains a `SKILL.md` file that defines behavior and triggers

## How to use install

To make the skill available to a skills.sh-compatible setup, point your local skills folder at this repository.

```sh
npx skills add FDiskas/auto-memory
```

## Skill behavior

The skill listens for prompts like:

- "remember this"
- "save to memory"
- "what do you remember about this?"
- "don't forget this"
- "important"
- "update memory"

It also checks memory at the start of relevant tasks, reading only the most relevant entries rather than loading everything.

## Example memory flow

```text
.claude/memory/
├── INDEX.md
├── project/
│   ├── INDEX.md
│   ├── caching/
│   │   ├── INDEX.md
│   │   └── lkg-key-collision.md
│   └── devcontainer/
│       ├── INDEX.md
│       └── firewall-dns-rotation.md
└── feedback/
    ├── INDEX.md
    └── pr-style.md
```

This keeps the history searchable, compact, and useful for follow-up work without turning the memory into a dump of raw session notes.

## Project status

This repository is ready to be used as a skill package in a skills.sh environment.

The main definition lives in [skills/auto-memory/SKILL.md](skills/auto-memory/SKILL.md), and the project-level guidance is in this README.
