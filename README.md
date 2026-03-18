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

BrainDump is designed to be driven by Claude — either through the CLI (Claude Code) or through Claude Desktop. Both give Claude full context of your ideas so you can manage them conversationally.

### Claude Code (CLI)

The fastest way to work with BrainDump. Claude Code reads `CLAUDE.md` automatically and understands all the conventions.

**Setup:**
```bash
# Clone the repo and open it with Claude Code
git clone <your-repo-url> BrainDump
cd BrainDump
claude
```

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

### Claude.ai Projects (claude.ai)

Claude.ai Projects let you persist `CLAUDE.md` as a standing instruction so every conversation in the project already knows the conventions — no re-pasting required.

**Setup:**

1. Go to [claude.ai](https://claude.ai) and create a new **Project** named "BrainDump".
2. In the project's *Instructions* field, paste the full contents of `CLAUDE.md`.
3. That's it. Every conversation in this project will follow the file conventions automatically.

When you want Claude to work on a specific idea, paste the relevant file contents directly into the chat (e.g. `idea.md`, `notes.md`). Claude will edit them and return the updated content for you to save back to disk.

**Example commands:**

```
# Capture a new idea (paste CLAUDE.md once if not in a project)
Create a new idea: "voice-memo-transcriber" — an iOS shortcut that transcribes
voice memos and saves them as markdown notes. Give me the three files to save.

# Review your ideas
[paste INDEX.md] — which ideas have been sitting in seed the longest?

# Deep-dive on one idea
[paste idea.md + notes.md] — suggest three concrete next steps for this idea

# Draft a journal entry
[paste notes.md] — add a note for today summarising the research I just described: ...
```

**Tip:** For a tighter workflow, combine Claude.ai for thinking and planning with Claude Code for actually writing the files and committing — use whichever fits the moment.

---

### Claude Code (Desktop)

Claude Code can also be launched from Claude Desktop via the integrated terminal. It has direct filesystem access and picks up `CLAUDE.md` automatically — no additional configuration needed.

**Setup:**

Open Claude Desktop, start an integrated terminal session, then:

```bash
cd /path/to/BrainDump
claude
```

Claude Code will read `CLAUDE.md` on startup and can read, write, and commit files directly. All the same CLI commands from the section above apply.

## Status Lifecycle

```
seed  →  active  →  done
                 →  abandoned
```

- **seed** — captured, not yet actively being developed
- **active** — currently being worked on or researched
- **done** — shipped, published, or otherwise complete
- **abandoned** — set aside (kept for reference, never deleted)
