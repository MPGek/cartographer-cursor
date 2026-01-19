# Cartographer - Cursor IDE Port

> **Fork:** This is a Cursor IDE port of [kingbootoshi/cartographer](https://github.com/kingbootoshi/cartographer) by MPGek.

## Codebase Overview

Cartographer is a codebase mapping tool that orchestrates parallel AI subagents to analyze and document codebases of any size. This version is specifically adapted for Cursor IDE.

**Stack**: Python 3.11, tiktoken, Markdown, Mermaid  
**Structure**: Cursor-native implementation using agent skills and subagents  

For detailed architecture, module breakdown, data flows, and navigation guides, see [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md).

## Quick Start (Cursor)

1. **Setup environment**:
   ```bash
   uv venv
   uv pip install -r requirements.txt
   ```

2. **Restart Cursor** (may be needed for skill to load)

3. **Invoke the skill**:
   - Type `/cartographer` in Agent chat
   - Or say "map this codebase"

## Key Features

- **Parallel subagent orchestration** - Splits work across multiple AI agents
- **Token-aware planning** - Analyzes codebase size and distributes optimally (~100k tokens per subagent)
- **Incremental updates** - Detects changes and only re-analyzes modified modules
- **Comprehensive documentation** - Generates architecture diagrams, module guides, data flows, and navigation guides
- **Respects .gitignore** - Only scans relevant source files

## Architecture

```
User → /cartographer → SKILL.md (orchestrator)
                          ↓
                    scan-codebase.py (token counter)
                          ↓
                    Plan subagent assignments
                          ↓
                    Spawn parallel subagents (Task tool)
                          ↓
                    Synthesize reports
                          ↓
                    Generate docs/CODEBASE_MAP.md
```

## Output

- **`docs/CODEBASE_MAP.md`** - Comprehensive codebase map with:
  - System overview and architecture diagrams
  - Directory structure with annotations
  - Module guide with file purposes, exports, dependencies
  - Data flow diagrams
  - Conventions and gotchas
  - Navigation guide for common tasks

## How It Works

Cartographer uses Cursor's Task tool to spawn parallel `explore` subagents with the `fast` model. Each subagent analyzes ~100k tokens of code and returns structured reports that are synthesized into comprehensive documentation.

## Original Project

Original work by Bootoshi: [kingbootoshi/cartographer](https://github.com/kingbootoshi/cartographer)

## License

MIT License
- **Original work:** Copyright (c) 2025 Bootoshi  
- **Fork modifications:** Copyright (c) 2026 MPGek

See [LICENSE](LICENSE) for full details.
