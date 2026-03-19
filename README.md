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

## Using with Claude

BrainDump is designed to be driven by Claude — either through the CLI (Claude Code) or through Claude Desktop - "Code" mode. Both give Claude full context of your ideas so you can manage them conversationally.

### Claude Code (CLI)

The fastest way to work with BrainDump. Claude Code reads `CLAUDE.md` automatically and understands all the conventions.

**Setup:**

```bash
# Clone the repo and open it with Claude Code
git clone <your-repo-url> BrainDump
cd BrainDump
claude
```

**Capture a new idea with the built-in skill:**

```
/new-idea
```

Claude will prompt you for the details and create all the files automatically.

**Example commands:**

```
# Capture a new idea
Create a new idea called "cli-tool-for-receipts" — a CLI that extracts line items from receipt photos using OCR

# Review what you have
Show me all my seed ideas and summarise each one in a sentence

# Start developing an idea
Move pinboard-ai-digest to active and add a note about my approach

# Work on to-dos
Add these tasks to pinboard-ai-digest: research Pinboard API auth, sketch email template

# Check progress
What's the status of all my active ideas?
```

**Tip:** Run `claude` from the `BrainDump/` directory so it picks up `CLAUDE.md` automatically. Claude will follow all the file conventions (append-only notes, never delete to-dos, correct commit format) without you having to repeat them.

---

### Claude Desktop - "Code" Mode

Claude Desktop's "Code" mode gives Claude direct filesystem access — no terminal needed. It picks up `CLAUDE.md` automatically when you open the repo as your working directory.

**Setup:**

1. Open Claude Desktop and switch to **Code** mode.
2. Set your working directory to the `BrainDump/` folder.
3. Start chatting — Claude will read `CLAUDE.md` and follow all conventions automatically.

All the same example commands from the CLI section above apply.

## Status Lifecycle

```
seed  →  active  →  done
                 →  abandoned
```

- **seed** — captured, not yet actively being developed
- **active** — currently being worked on or researched
- **done** — shipped, published, or otherwise complete
- **abandoned** — set aside (kept for reference, never deleted)
