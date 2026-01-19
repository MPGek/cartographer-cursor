# Codebase Summary

**Cartographer** is a codebase mapping tool for Cursor IDE that orchestrates parallel AI subagents to analyze and document codebases of any size. The main orchestrator delegates file reading to subagents, which analyze assigned files and return structured reports that are synthesized into comprehensive documentation.

**Stack**: Python 3.11, tiktoken, Markdown, Mermaid diagrams, Cursor Task tool API

**Structure**: The skill orchestrates via `.cursor/skills/cartographer/SKILL.md`, the scanner counts tokens via `scan-codebase.py`, and parallel subagents analyze files using the `codebase-analyzer.md` template. Output is written to `docs/CODEBASE_MAP.md` with architecture diagrams, module guides, data flows, and navigation information.

**📖 Full Architecture Map**: [docs/CODEBASE_MAP.md](docs/CODEBASE_MAP.md)
