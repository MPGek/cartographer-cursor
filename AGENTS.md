# Agents & Skills

This repository contains specialized Cursor agents and skills designed for advanced codebase management.

## Cartographer

**Summary**: A powerful orchestration skill that maps and documents codebases of any size using parallel subagents. It automatically analyzes architecture, file purposes, and dependencies.

- **Stack**: Python (Scanner), Markdown (Orchestration), Cursor Task Tool (Subagents).
- **Structure**:
  - Orchestrator: `.cursor/skills/cartographer/SKILL.md`
  - Scanner: `.cursor/skills/cartographer/scripts/scan-codebase.py`
  - Subagent: `.cursor/agents/codebase-analyzer.md`
- **Full Map**: See [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md) for the complete architecture map.

---
*Last updated: 2026-01-19*
