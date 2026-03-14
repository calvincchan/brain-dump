---
allowed-tools: Read, Write, Edit, Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(mkdir:*)
description: Create a new idea in BrainDump from templates
argument-hint: [idea title]
---

Create a new BrainDump idea by following these steps exactly.

## Step 1 — Determine title and slug

- If `$ARGUMENTS` is non-empty, use it as the title.
- If `$ARGUMENTS` is empty, ask the user for the title before proceeding.
- Derive the kebab-case slug: lowercase, spaces → hyphens, strip all punctuation except hyphens.
  - Example: "My Great Idea!" → `my-great-idea`

## Step 2 — Get today's date

Run `date +%Y-%m-%d` to get today's date. Use this value for all date fields.

## Step 3 — Create the idea directory

```
mkdir -p ideas/<slug>
```

## Step 4 — Create `ideas/<slug>/idea.md`

Write the file with this exact content, substituting the placeholders:

```
---
id: <slug>
title: <title>
status: seed
tags: []
created: <today>
updated: <today>
---

## What Is This?

<!-- A clear, concise description of the idea. What does it do or produce? -->

## Why Does It Matter?

<!-- What problem does it solve, or what value does it create? Who would benefit? -->

## Key Context

<!-- Background knowledge, prior art, constraints, or anything relevant to understanding this idea. -->
```

## Step 5 — Create `ideas/<slug>/notes.md`

Write the file with this exact content, substituting `<today>` with today's date:

```
# Notes

Append-only development journal. Add new entries at the **top**, below this heading.
Never edit or delete existing entries.

---

## <today>

Initial capture. Idea created from template.
```

## Step 6 — Create `ideas/<slug>/todo.md`

Write the file with this exact content verbatim:

```
# To-Do

Never delete completed items — mark them `[x]` and leave them in place.

- [ ] Define the idea clearly in `idea.md`
- [ ] Identify the first concrete next step
- [ ] Research unknowns and open questions
```

## Step 7 — Update `INDEX.md`

Read `INDEX.md` and insert a new row into the **Seed** table. The new row format is:

```
| [<title>](ideas/<slug>/idea.md) | <slug> | _(none)_ | <today> | <today> |
```

Insert the row so the Seed table remains sorted by Updated date descending (newest first). If there is a `_(none yet)_` placeholder row, replace it with the new row.

## Step 8 — Commit

Stage and commit the new files:

```
git add ideas/<slug>/ INDEX.md
git commit -m "idea: add <slug>"
```

## Step 9 — Confirm

Tell the user the idea was created, showing:
- The slug and title
- The path to the idea file: `ideas/<slug>/idea.md`
