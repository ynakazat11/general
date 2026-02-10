# My CLAUDE.md

Global configuration file for [Claude Code](https://code.claude.com). Lives at `~/.claude/CLAUDE.md` and applies to every project.

## Setup

```bash
mkdir -p ~/.claude
cp CLAUDE.md ~/.claude/CLAUDE.md
```

## Design Principles

This file was built following researched best practices, not vibes.

### Keep it brutally short

- Claude Code's system prompt already consumes ~50 of the ~150-200 instructions frontier models can reliably follow ([source](https://www.humanlayer.dev/blog/writing-a-good-claude-md), [paper](https://arxiv.org/pdf/2507.11538))
- As instruction count increases, compliance degrades **uniformly** — it doesn't just ignore the bottom of the file, it starts ignoring everything
- Target: **under 60 lines**. HumanLayer's production file is under 60. This one is 40.

### Only universally applicable rules

Claude Code wraps your CLAUDE.md with a system note that says to ignore it if not relevant to the current task. The more project-specific junk you put in the global file, the more likely Claude ignores the important stuff too. If a rule doesn't apply to every single project you work on, it doesn't belong here.

### Don't do a linter's job

No formatting rules, no import ordering, no indentation preferences. Use `ruff`, `black`, or similar as a [PostToolUse hook](https://code.claude.com/docs/en/hooks) — deterministic, fast, free. Claude is expensive and slow at formatting by comparison.

### Progressive disclosure over front-loading

Instead of dumping all docs into context, point Claude to where docs live and let it read them when relevant. This keeps context clean for the actual task.

### No personality prompts

"Be a senior engineer" or "Think step by step" wastes tokens. Claude Code already has strong system-level behavioral instructions.

## File Hierarchy

```
~/.claude/CLAUDE.md          ← THIS FILE (global, all projects)
/project-root/CLAUDE.md      ← Project-specific (shared with team, in git)
/project-root/CLAUDE.local.md ← Personal overrides (gitignored)
/project-root/src/*/CLAUDE.md ← Directory-specific (loaded on demand)
```

All levels combine. More specific levels override on conflicts. Project CLAUDE.md overrides global; local overrides project.

## How to Evolve

**Add corrections live:** Press `#` during a Claude Code session to save a lesson directly to CLAUDE.md. Over time the file compounds — every mistake becomes permanent context.

**Prune regularly:** If this file creeps past 60 lines, something probably belongs in a project-level file. Review monthly.

**Never auto-generate:** `/init` is fine for project-level files as a starting point. But this global file is the highest-leverage point in your entire Claude Code setup — every line affects every session. Craft it deliberately.

## Forking for Work

When adapting for a work repo:

1. Copy this file as a starting point for the **project-level** `CLAUDE.md`
2. Replace generic preferences with project-specific context:
   - What the project is (one line)
   - Key directories and what they contain
   - Essential commands (build, test, lint, deploy)
   - Gotchas and danger zones (auth, payments, migrations)
3. Keep a `CLAUDE.local.md` (add to `.gitignore`) for personal setup
4. Commit the project `CLAUDE.md` to git — the whole team contributes

## Key Sources

- [HumanLayer: Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) — best single article on the topic
- [Boris Cherny's workflow](https://howborisusesclaudecode.com/) — creator of Claude Code, his actual setup
- [Anthropic: Using CLAUDE.md files](https://claude.com/blog/using-claude-md-files) — official guide
- [Shrivu Shankar: How I Use Every Feature](https://blog.sshh.io/p/how-i-use-every-claude-code-feature) — advanced patterns, CLAUDE.md as forcing function
- [Builder.io: Complete Guide to CLAUDE.md](https://www.builder.io/blog/claude-md-guide) — practical examples
