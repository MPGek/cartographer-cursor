# Cartographer for Cursor IDE

> **Note:** This is a Cursor IDE port of [kingbootoshi/cartographer](https://github.com/kingbootoshi/cartographer), adapted to work with Cursor's agent skills and subagents system.

<img width="640" height="360" alt="cartographer" src="https://github.com/user-attachments/assets/542818c6-fc2b-41a6-915d-cf196447f346" />

Maps and documents codebases of any size using parallel AI subagents in Cursor IDE.

## Prerequisites

### Enable Cursor Beta Features

Cartographer requires Cursor's **agent skills** and **subagents** features, which are available in the **Nightly** release channel.

**To enable:**

1. Open Cursor Settings (`Cmd+Shift+J` on Mac, `Ctrl+Shift+J` on Windows/Linux)
2. Select **Beta** tab
3. Set update channel to **Nightly**
4. Restart Cursor to apply the update

## Installation

### Quick Install

1. Clone this repository to a temporary folder:

```bash
git clone https://github.com/MPGek/cartographer-cursor.git /tmp/cartographer-cursor
```

2. Copy the `.cursor` folder to your project:

```bash
# Copy to your project root
cp -r /tmp/cartographer-cursor/.cursor /path/to/your/project/

# Clean up (optional)
rm -rf /tmp/cartographer-cursor
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/MPGek/cartographer-cursor.git $env:TEMP\cartographer-cursor
Copy-Item -Recurse $env:TEMP\cartographer-cursor\.cursor -Destination .
Remove-Item -Recurse -Force $env:TEMP\cartographer-cursor
```

### Global Install (All Projects)

To use Cartographer across all your projects, copy to your user-level `.cursor` folder:

```bash
# macOS/Linux
cp -r /tmp/cartographer-cursor/.cursor ~/.cursor

# Windows (PowerShell)
Copy-Item -Recurse $env:TEMP\cartographer-cursor\.cursor -Destination $env:USERPROFILE\.cursor
```

### Restart Cursor

After installation, restart Cursor IDE for the skill to load.

## Usage

Invoke the cartographer skill in Cursor Agent chat:

```
/cartographer
```

Or use natural language:
- "map this codebase"
- "create codebase map"
- "document the architecture"

## What it Does

Cartographer orchestrates multiple fast subagents via Cursor's Task tool to analyze your entire codebase in parallel, then synthesizes their findings into:

- **`docs/CODEBASE_MAP.md`** - Comprehensive architecture map with:
  - System overview with mermaid diagrams
  - Directory structure with annotations
  - Module guides with file purposes, exports, dependencies
  - Data flow diagrams
  - Conventions and gotchas
  - Navigation guide for common tasks

- **`AGENTS.md`** - Summary with link to the detailed map

## How it Works

1. Runs scanner script to get file tree with token counts (respects `.gitignore`)
2. Plans how to split work across subagents based on token budgets (~100k tokens per subagent)
3. Spawns subagents in parallel using Cursor's Task tool (`explore` type, `fast` model)
4. Synthesizes all subagent reports into comprehensive documentation

## Update Mode

If `docs/CODEBASE_MAP.md` already exists, Cartographer will:

1. Check git history for changes since last mapping
2. Only re-analyze changed modules
3. Merge updates with existing documentation

Just run `/cartographer` again to update.

## Token Usage

Cartographer uses Cursor's `fast` model for subagents to balance cost and capability. Token usage depends on codebase size.

## Requirements

- **Cursor IDE Nightly** (for agent skills & subagents)
- **Python 3.11+**
- **tiktoken** (for token counting) - auto-installed via `uv run` or install manually: `uv pip install tiktoken`
- **UV** (recommended) - Python package manager

## Key Differences from Original

This Cursor port differs from the original Claude Code plugin:

| Aspect | Cursor Version | Original (Claude Code) |
|--------|---------------|------------------------|
| Platform | Cursor IDE Nightly | Claude Code |
| Location | `.cursor/` | `.claude/` |
| Subagent API | Task tool (`explore` type) | Claude native subagents |
| Model | `fast` | `sonnet` |
| Token Budget | ~100k per subagent | ~150k per subagent |
| Output File | `AGENTS.md` | `CLAUDE.md` |
| Setup | Clone to `.cursor/` | Plugin marketplace install |

## Documentation

- [AGENTS.md](AGENTS.md) - Quick reference for Cursor usage
- [docs/CODEBASE\_MAP.md](docs/CODEBASE_MAP.md) - Comprehensive codebase map (generated after first run)

## Original Project

Original project by Bootoshi: [kingbootoshi/cartographer](https://github.com/kingbootoshi/cartographer)

## License

MIT License - See [LICENSE](LICENSE) for details

**Original work:** Copyright (c) 2025 Bootoshi
**Fork modifications:** Copyright (c) 2026 MPGek
