# BrainDump — Agent Operating Manual

This file defines the contract for Claude Code and other AI agents working in this repository. Follow these rules consistently across all sessions.

---

## Repository Structure

```
BrainDump/
├── CLAUDE.md                  # This file — agent operating manual
├── README.md                  # Human-facing overview
├── INDEX.md                   # Dashboard: all ideas listed by status
├── _templates/
│   └── new-idea/
│       ├── idea.md            # Template: frontmatter + description sections
│       ├── notes.md           # Template: append-only journal
│       └── todo.md            # Template: checkbox to-do list
└── ideas/                     # One subdirectory per idea
    └── <kebab-case-slug>/
        ├── idea.md            # Canonical description + YAML frontmatter
        ├── notes.md           # Append-only development journal
        └── todo.md            # GitHub-flavoured checkbox to-do list
```

---

## File Rules

### `idea.md` — Source of Truth

- Contains YAML frontmatter (metadata) and the canonical description of the idea.
- **Only update frontmatter fields when:** the status changes, tags are added/removed, or the description is meaningfully revised.
- Always update the `updated` field to today's date when making any change to `idea.md`.
- Never delete or rename the file; the slug must match the parent directory name.

**Frontmatter schema:**
```yaml
---
id: slug-matching-directory-name
title: Human-Readable Title
status: seed          # seed | active | done | abandoned
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Status lifecycle:** `seed → active → done` or `seed → active → abandoned`

### `notes.md` — Append-Only Journal

- **Never edit or delete existing entries.** Only prepend new entries at the top (below the heading).
- Each entry begins with a `## YYYY-MM-DD` date heading.
- Use for: development thinking, research findings, decisions made, progress updates.
- Multiple entries on the same day are allowed; use a single date heading with subsections if needed.

### `todo.md` — Checkbox List

- Use GitHub-flavoured Markdown checkboxes: `- [ ] item` and `- [x] done item`.
- **Never delete completed items** — mark them done with `[x]` and leave them in place.
- Add new items at the bottom of the relevant section, or at the top if no sections exist.
- Group related items with `### Section` headings if the list grows long.

---

## How to Create a New Idea

1. Choose a `kebab-case-slug` for the idea (short, descriptive, no dates).
2. Create the directory: `ideas/<slug>/`
3. Copy all three template files from `_templates/new-idea/` into `ideas/<slug>/`.
4. Fill in the frontmatter in `idea.md`:
   - Set `id` to the slug.
   - Set `title` to the human-readable title.
   - Set `status` to `seed`.
   - Set `tags` to relevant tags (can be empty: `[]`).
   - Set `created` and `updated` to today's date.
5. Fill in the description sections in `idea.md` below the frontmatter.
6. Add the idea to `INDEX.md` under the **Seed** table.
7. Commit: `idea: add <slug>`

---

## How to Maintain INDEX.md

`INDEX.md` is the dashboard. Keep it accurate whenever statuses change.

- When **creating** an idea: add a row to the appropriate status table.
- When **changing status**: move the row to the new status table and update the Status column.
- Column order: `| Title | Slug | Tags | Created | Updated |`
- Titles should link to the idea file: `[Title](ideas/<slug>/idea.md)`
- Keep rows sorted by `Updated` date descending within each table.

---

## Commit Message Conventions

| Action | Format |
|---|---|
| Create new idea | `idea: add <slug>` |
| Update description | `idea(<slug>): update description` |
| Change status | `idea(<slug>): status → <new-status>` |
| Add notes | `idea(<slug>): add notes` |
| Update to-do | `idea(<slug>): update todo` |
| Multiple changes | `idea(<slug>): <summary of changes>` |
| System/structural changes | `system: <description>` |

---

## Autonomous vs. Approval-Required Actions

### Agents MAY do autonomously:
- Create a new idea from template when asked.
- Add, update, or reorganize `todo.md` items.
- Prepend new entries to `notes.md`.
- Update `INDEX.md` to reflect status changes.
- Update `updated` date in frontmatter.
- Create commits following the conventions above.

### Agents MUST ask for user approval before:
- Changing an idea's status (especially to `done` or `abandoned`).
- Deleting any file.
- Modifying existing `notes.md` entries (not appending — editing old ones).
- Pushing commits to a remote.
- Making bulk changes across multiple ideas in one action.

---

## Finding All Ideas

To find all ideas: glob `ideas/*/idea.md` — each file's frontmatter is the metadata source of truth.

To find ideas by status: read `INDEX.md` for a quick overview, or grep frontmatter for `status: <value>`.
