# CLAUDE.md — Embodied Intelligence Weekly Digest

This file provides guidance to Claude Code (claude.ai) when working with this repository.

## Project overview

**Embodied Intelligence Weekly Digest** (具身智能每周发展摘要) is a weekly report on global embodied AI and humanoid robot developments. It collects events from 30+ information sources across 12 ecosystem groups, scores them on a 5-dimension impact scale, and publishes AI-generated Chinese deep analysis.

This project inherits methodology from `github-weekly-digest` — same configuration/prompt separation, same LLM graceful degradation, same GitHub Actions deployment pattern.

## Architecture

```
30 sources → RealSearchCollector → Merge/Dedup → 5-dim Score → DeepAnalyzer (LLM) → MarkdownRenderer → GitHub Actions commit
                    (12 ecosystems, Tier 1/2)      |                 |                   |
                                                    v                 v                   v
                                               Confidence A/B/C/D  "No naked jargon"   weekly/YYYY-NN.md
                                                                    2-layer reading
```

## Key modules

| Module | Path | Purpose |
|--------|------|---------|
| Collectors | `src/collectors/` | `base.py` (EventRecord, SourceCitation, BaseCollector), `web_search.py` (RealSearchCollector — keyword-based event discovery) |
| Filters | `src/filters/` | `dedup.py` (JSON state file dedup), `quality.py` (basic title+citation check), `scorer.py` (cross-ecosystem independence scoring) |
| AI | `src/ai/` | `llm_client.py` (multi-provider: Gemini/DeepSeek/Qwen/Anthropic/OpenAI), `deep_analyzer.py` (weekly analysis), `feedback_loader.py` |
| Render | `src/render/` | `markdown_weekly.py` (weekly report + category index) |
| Config | `config/` | `sources.yml` (30 sources, 12 ecosystems), `keywords.yml`, `quality.yml` (5-dim weights + 6 categories) |
| Prompts | `prompts/` | `weekly-deep.md`, `taxonomy.md`, `feedback-rules.md` |
| Orchestrator | `src/main.py` | Pipeline: collect → merge → dedup → filter → score → AI → render |

## Data flow

1. **Collect**: `RealSearchCollector` generates EventRecords from each source's keyword list. Each record carries a SourceCitation with tier + ecosystem.
2. **Merge**: Records with identical event_id merge citation chains.
3. **Dedup**: `Deduplicator` checks JSON state file — already-seen events are skipped.
4. **Filter**: `QualityFilter` ensures every record has a title and at least one citation.
5. **Score**: `Scorer` computes confidence from cross-ecosystem citations. Tier 1 = 40pts, Tier 2 = 25pts, multiplied by ecosystem independence_weight, capped at 100.
6. **AI**: `DeepAnalyzer` sends top 15 events + taxonomy + feedback rules to LLM. Falls back to data-only table on failure.
7. **Render**: `MarkdownRenderer` produces `output/weekly/{year}/{YYYY-WNN}.md` with frontmatter, AI analysis, top-N table, and category sections.

## Quick start

```bash
# Install
pip install -r requirements.txt

# Run (data-only, no LLM needed)
python run.py --mode weekly

# Run with AI summaries
export GEMINI_API_KEY="your-key-here"
python run.py --mode weekly
```

## Deployment

- **Workflow**: `.github/workflows/weekly-digest.yml` — cron `37 10 * * 1` (Mon 18:37 CST)
- **Watchdog**: `.github/workflows/watchdog.yml` — 3× Monday checks
- **Secrets needed**: `GH_TOKEN` (repo + workflow scope), `GEMINI_API_KEY`
- **Concurrency group**: `embodied-weekly`, no cancel-in-progress

## 5-dimension scoring

| Dimension | Weight | What it measures |
|-----------|--------|------------------|
| Industry Disruption | 30% | Reshaping potential for embodied AI landscape |
| Technical Breakthrough | 25% | Novelty and difficulty of the achievement |
| Commercialization | 20% | Mass production, delivery, funding, IPO |
| Ecosystem Impact | 15% | Effect on developers, supply chain, downstream |
| Policy & Capital | 10% | Government policy, investment signals |

## 6 category labels

`#hardware` (robot platforms), `#vla-model` (VLA/algorithms), `#simulation` (sim-to-real/data), `#manipulation` (dexterous ops/perception), `#industry` (commercialization), `#policy` (regulation)

## Important design decisions

- **RealSearchCollector**: Unlike github-weekly-digest which scrapes GitHub Trending, embodied AI events come from distributed sources. The collector uses pre-configured keyword lists per source — in production these would hit real search APIs, but the architecture supports AI enrichment of keyword-hit data.
- **30 sources in 12 ecosystems**: More than github-weekly-digest (8) because no single "GitHub Trending" exists for embodied AI. Heavy Chinese/English ecosystem divide.
- **LLM graceful degradation**: If no API key is set, the pipeline produces data-only reports — never blocks.
- **All imports are absolute**: `from src.collectors.base import ...` — compatible with `run.py` at repo root.

## Related projects

- `../github-weekly-digest/` — Methodology source (Python pipeline, GitHub Actions deployment)
- `../multimodal-ai-weekly/` — Same-format sibling (Multimodal AI)
- `../领域知识自动化收集评价存储部署发布-完整方法论.md` — Universal methodology guide
