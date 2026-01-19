# Agents & Skills

This repository contains specialized Cursor agents and skills designed for advanced codebase management.

## Cartographer

**Summary**: A powerful orchestration skill that maps and documents codebases of any size using parallel AI subagents. It solves the context window limitation by dividing codebases into manageable chunks (~100k tokens each), analyzing them in parallel via Cursor's Task tool, and synthesizing results into comprehensive documentation.

**Key Features**:
- Automatic change detection (git-based or file comparison)
- Parallel subagent execution for speed
- Incremental updates preserve unchanged sections
- Token budget management prevents context overflow
- Generates Mermaid architecture diagrams
- Creates navigation guides for common tasks

**Stack**: 
- Python (Scanner with tiktoken for token counting)
- Markdown (Orchestration workflow)
- Cursor Task Tool (Parallel subagent spawning)

**Structure**:
- Orchestrator: `.cursor/skills/cartographer/SKILL.md`
- Scanner: `.cursor/skills/cartographer/scripts/scan-codebase.py`
- Subagent: `.cursor/agents/codebase-analyzer.md`

**Usage**: Type `/cartographer` in Cursor chat or use natural language triggers like "map this codebase" or "document the architecture".

**Requirements**: Cursor Nightly, Python 3.9+, UV recommended.

**Full Map**: See [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md) for the complete architecture map with detailed module guides, data flows, conventions, and troubleshooting.

---

## Codebase Overview

This repository provides the Cartographer skill for Cursor - a codebase mapping tool that uses orchestration patterns to analyze codebases of any size. The main agent coordinates work, while specialized subagents perform read-only analysis in parallel, ensuring efficient processing without hitting context limits.

**Current Codebase**:
- 7 files, 8,525 tokens
- 3 core components (Orchestrator, Scanner, Analyzer)
- MIT Licensed
- Last mapped: 2026-01-19

For detailed architecture, see [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md).

---
*Last updated: 2026-01-19*
