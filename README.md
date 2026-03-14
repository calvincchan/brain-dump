# BrainDump

A personal, text-based idea management system. Every idea lives in its own directory as plain Markdown files — versioned with git, readable by humans and AI agents alike.

---

## Why This Exists

Ideas deserve better than a notes app graveyard. This repo gives each idea:
- A canonical description with metadata
- An append-only development journal
- A to-do list that preserves history

Everything is plain Markdown. Git provides the full history. No app lock-in.

---

## Structure

```
ideas/<slug>/
├── idea.md      # What the idea is and why it matters (+ YAML metadata)
├── notes.md     # Running journal — newest entries at top
└── todo.md      # Checkboxes — completed items are never deleted
```

Browse all ideas in [INDEX.md](INDEX.md).

---

## How to Add a New Idea

1. Pick a short `kebab-case-slug` for the idea.
2. Copy `_templates/new-idea/` to `ideas/<slug>/`.
3. Fill in `idea.md` — frontmatter fields and description sections.
4. Add a row to the **Seed** table in `INDEX.md`.
5. Commit: `idea: add <slug>`

Full agent instructions are in [CLAUDE.md](CLAUDE.md).

---

## Status Lifecycle

```
seed  →  active  →  done
                 →  abandoned
```

- **seed** — captured, not yet actively being developed
- **active** — currently being worked on or researched
- **done** — shipped, published, or otherwise complete
- **abandoned** — set aside (kept for reference, never deleted)
