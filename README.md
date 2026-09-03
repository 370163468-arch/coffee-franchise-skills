# Coffee Franchise Skills for OPC Studio

This repository contains curated **skill packs** for OPC Studio's "coffee franchise" workflow template. OPC workers load these skills at runtime to bring domain expertise to their analysis.

## Skills

| Skill | Purpose | Used by worker |
|-------|---------|----------------|
| [market-research](./market-research/SKILL.md) | Industry sizing, competitor benchmarking, consumer trends, brand selection criteria | `cafe_market_analyst` |
| [finance-model](./finance-model/SKILL.md) | Capex, P&L forecast, break-even, ROI scenarios, 3-year exit analysis | `cafe_finance_planner` |
| [location-eval](./location-eval/SKILL.md) | Foot-traffic, catchment, competitor proximity, rent sanity, 100-point scoring | `cafe_location_evaluator` |

## How skills are consumed

OPC Studio clones this repo (sparse, per-skill) into `~/.kong-agent-platform/skills/<skill-name>/` and appends each skill's `SKILL.md` content to the worker's system prompt. The worker then operates as a domain expert for the task.

Each skill is in its **own directory** so the runtime can do sparse checkout via `git clone --filter=blob:none --sparse` plus `git sparse-checkout set <skill-name>`.

## Contributing

Each `SKILL.md` follows the OpenClaw SKILL.md format:
- YAML frontmatter (`name`, `description`)
- "When to use this skill"
- Inputs the worker should expect
- Mandatory framework sections
- Output format spec
- Quality bar
- Explicit "what this skill does NOT do" boundary

Skills should be **tightly scoped** — defer to other skills, never duplicate.

## Repository metadata

- **Owner:** @370163468-arch
- **License:** MIT (intended)
- **Created:** 2026-09-03
- **Source workspace:** `D:\kong-agent-platform\backend\workers\skills_github.py` (loader), `D:\kong-agent-platform\backend\opc_api.py` (clone API)