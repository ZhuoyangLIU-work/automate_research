# Automate Research

A Claude skill for deep academic literature research and synthesis. Given a set of papers (or just a topic), it runs a systematic 9-step protocol that goes far beyond summarization -- finding contradictions, tracing citation chains, scanning for gaps, auditing methodologies, and surfacing hidden assumptions.

## Two Versions

### `literature-researcher/` (Condensed -- Recommended)
203 lines. Tighter instructions, better test performance, faster execution, fewer tokens. Start here.

### `literature-researcher-verbose/` (Verbose)
351 lines. Same protocol with more detailed explanations and examples at each step. Use this if you want the skill to have more guidance on edge cases.

## The 9-Step Protocol

1. **Intake Protocol** -- Catalog papers with a unified indexing system (`NNN-S/D-YYYY-Author-Title`), cluster by assumptions, expand small seed sets via web search
2. **Contradiction Finder** -- Identify direct contradictions between authors, diagnose why they disagree
3. **Citation Chain** -- Trace the intellectual lineage of the 3 most-cited concepts, with Mermaid diagrams
4. **Gap Scanner** -- Find the 5 most significant unanswered research questions, ranked by impact
5. **Methodology Audit** -- Compare methods across papers, find what dominates, what's underused, what's weakest
6. **Master Synthesis** -- Field-level synthesis (max 500 words) of consensus, debates, and proven claims
7. **Assumption Killer** -- Surface hidden assumptions the field relies on but never tests
8. **Knowledge Map** -- Structured outline of the field's architecture with Mermaid diagram
9. **"So What" Test** -- Plain-language summary for a smart non-expert

## Features

- **Unified paper indexing** -- Every paper gets a traceable code (e.g., `[001-S]`, `[003-D]`) used consistently across all 9 steps
- **Web search integration** -- Searches Google Scholar, arXiv, top lab blogs (DeepMind, OpenAI, Anthropic, etc.), SSRN, and paywalled databases via institutional library access
- **Visual outputs** -- Mermaid diagrams for citation chains and knowledge maps
- **Flexible execution** -- Run all steps automatically, pause at checkpoints, or go step-by-step

## Installation

**Option A — Copy the skill folder (recommended)**

Clone this repo (or download the folder) and copy your preferred version into your Claude skills directory:

```bash
# Condensed (recommended)
cp -r literature-researcher/ ~/.skills/skills/

# Verbose
cp -r literature-researcher-verbose/ ~/.skills/skills/
```

Each folder contains a single `SKILL.md` file, which is all Claude needs to load the skill.

**Option B — Use the .skill package**

Download the `.skill` file from this repo and install it via the Claude desktop app.

## License

MIT

## Acknowledgments

The 9-step protocol used in this skill was inspired by a prompt framework originally shared by [Jainam Parmar (@aiwithjainam) on X](https://x.com/aiwithjainam), which outlined a set of research prompts for turning Claude into a literature research co-pilot. The step names (Contradiction Finder, Citation Chain, Gap Scanner, Assumption Killer, etc.) and overall structure originate from that work.
