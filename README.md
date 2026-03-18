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

### Claude Desktop

Claude Desktop works best with the **MCP filesystem server**, which lets Claude read and write your local files directly — no copy-pasting required.

**Setup:**

1. Install the MCP filesystem server (if not already available in your Claude Desktop config):
   ```bash
   npm install -g @modelcontextprotocol/server-filesystem
   ```

2. Open Claude Desktop settings and add the server to your `claude_desktop_config.json`:
   ```json
   {
     "mcpServers": {
       "braindump": {
         "command": "npx",
         "args": [
           "-y",
           "@modelcontextprotocol/server-filesystem",
           "/absolute/path/to/BrainDump"
         ]
       }
     }
   }
   ```
   Replace `/absolute/path/to/BrainDump` with your actual path (e.g. `/Users/yourname/BrainDump`).

3. Restart Claude Desktop. You should see the filesystem server listed as an active tool.

4. Start a conversation and paste the contents of `CLAUDE.md` into your first message (or save it as a Project instruction if you have Claude Pro/Teams). This primes Claude with all the conventions.

**Example commands:**

```
# Capture an idea
Read my CLAUDE.md and then create a new idea: "voice-memo-transcriber" —
an iOS shortcut that transcribes voice memos and saves them as markdown notes

# Review your index
Read INDEX.md and tell me which ideas have been sitting in seed for the longest

# Deep-dive on one idea
Read ideas/pinboard-ai-digest/idea.md and notes.md, then suggest three concrete next steps

# Tidy up
Read all idea.md files and tell me which ones are missing tags
```

**Tip:** If you use Claude Pro, create a **Project** for BrainDump and add `CLAUDE.md` as a project instruction. Claude will then know the conventions for every conversation without you having to re-paste it.

## Status Lifecycle

```
seed  →  active  →  done
                 →  abandoned
```

- **seed** — captured, not yet actively being developed
- **active** — currently being worked on or researched
- **done** — shipped, published, or otherwise complete
- **abandoned** — set aside (kept for reference, never deleted)
