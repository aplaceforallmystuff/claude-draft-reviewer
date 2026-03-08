# Claude Draft Reviewer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Agent-blue)](https://claude.ai)

A Claude Code agent that reviews AND FIXES drafts for AI slop, writing craft, and voice consistency. Unlike traditional reviewers that just report issues, this agent applies all fixes directly.

## The Problem

Content reviewers typically produce reports listing issues for you to fix. This creates:

- Manual work translating suggestions to edits
- Risk of missing items in the list
- Inconsistent application of fixes
- Extra round-trips between review and implementation

This agent eliminates that gap by being a **fixer, not just a reporter**.

## How It Works

The agent runs a 3-phase workflow:

| Phase | Action | Output |
|-------|--------|--------|
| 1. Analysis | Runs three quality checks | Issues identified |
| 2. Apply Fixes | Uses Edit tool on each issue | Content modified |
| 3. Report | Summarizes changes made | Before/after log |

### Quality Checks

1. **Slop Detection** - Identifies AI-generated patterns (requires `slop-detector` skill)
2. **Craft Rules Audit** - Checks writing mechanics (requires `craft-rules` skill)
3. **Voice Check** - Validates voice consistency (requires `voice-editor` skill)
4. **Factual Accuracy** - Verifies claims in first-person/experiential content against source material

### Optional: Local LLM Cost Optimization

If you have a local LLM available (e.g., via Ollama), the agent can run a quick pre-scan to classify drafts by severity before running full analysis. This can reduce token costs by 40-50% for clean drafts. See the agent file's `<cost_optimization>` section for details.

## Prerequisites

This agent requires three companion skills to function:

- [`slop-detector`](https://github.com/aplaceforallmystuff/claude-slop-detector) - AI pattern detection
- [`craft-rules`](https://github.com/aplaceforallmystuff/claude-craft-rules) - Writing mechanics (if published)
- [`voice-editor`](https://github.com/aplaceforallmystuff/claude-voice-editor) - Voice consistency

Install the required skills before using this agent.

## Installation

### Option 1: Copy to your Claude Code agents directory

```bash
# Clone the repository
git clone https://github.com/aplaceforallmystuff/claude-draft-reviewer.git

# Copy to your Claude Code agents directory
cp claude-draft-reviewer/agents/draft-reviewer.md ~/.claude/agents/
```

### Option 2: Clone directly to agents directory

```bash
git clone https://github.com/aplaceforallmystuff/claude-draft-reviewer.git ~/.claude/agents/draft-reviewer
```

### Option 3: Manual installation

1. Create the directory: `mkdir -p ~/.claude/agents`
2. Download [draft-reviewer.md](agents/draft-reviewer.md) to that directory

## Usage

The agent activates when you say:

- "review this draft"
- "check my writing"
- "audit content"

Or invoke directly with `@draft-reviewer`

### Example Session

```
User: @draft-reviewer review this blog post [paste content]

Agent: Running quality checks...

[Invokes slop-detector]
[Invokes craft-rules]
[Invokes voice-editor]

Applying fixes...

[Edit: "delve into" → "examine"]
[Edit: "In today's fast-paced world" → removed]
[Edit: passive voice → active voice]

# Draft Review + Edit Report

## Quick Summary
- **Slop Score:** 45/100 → 12/100 after fixes
- **Craft Score:** 9/16 → 14/16 after fixes
- **Voice Match:** 70% → 92%
- **Edits Applied:** 8 changes made

[detailed before/after log...]
```

## What Gets Fixed Automatically

| Category | Examples |
|----------|----------|
| Tier 1 Slop | "delve", "landscape", "game-changer" |
| Tier 2 Slop | "leverage", "robust", "seamless" |
| Passive Voice | "was implemented" → "implemented" |
| Staccato Fragments | Short. Choppy. Sentences. → Combined |
| Weak Openings | Generic intros → Specific hooks |
| Abstract Adjectives | "innovative" → specific details |

## What Gets Flagged (Not Auto-Fixed)

- Tone choices that could go either way
- Major structural reorganization
- Content additions or deletions
- Anything that changes meaning
- Unverifiable factual claims in first-person content (removed or genericized rather than left in)

## Configuration

The agent uses Sonnet model by default for optimal speed/quality balance.

### Tools Required

- `Read` - Read draft content
- `Write` - Create new files if needed
- `Edit` - Apply fixes
- `Skill` - Invoke quality check skills
- `Glob` - Find files

## Philosophy

> **Editors, not critics.**

Traditional review processes separate analysis from implementation. This agent merges them:

1. Find an issue
2. Fix it immediately
3. Report what changed

No suggestions. No recommendations. Just fixes with explanations.

## License

MIT License - see [LICENSE](LICENSE)

---

**The goal: Clean drafts, not clean reports about dirty drafts.**
