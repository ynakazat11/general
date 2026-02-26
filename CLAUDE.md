# Global Preferences

## Identity
- I work primarily in Python (FastAPI, Flask, scripting, ML/AI tooling)
- I use Neovim as my editor and zsh as my shell
- I maintain projects on GitHub

## Core Principles
- Simplicity first — make every change as simple as possible, impact minimal code
- No laziness — find root causes, no temporary fixes, staff-engineer standards
- Minimal impact — changes should only touch what's necessary
- Prefer simple, readable code over clever abstractions
- Prefer composition over inheritance

## Code Quality
- Type hints required on all function signatures
- Use dataclasses or Pydantic models over raw dicts for structured data
- Small functions that do one thing; if a function needs a comment explaining "what", it's too complex
- Handle errors explicitly — no bare `except:`, no silent failures
- Don't use `os.system()` — use `subprocess.run()` with proper error handling

## Execution Strategy
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- For multi-step plans, implement in small batches (2-4 steps per batch)
- In plan mode, the plan header must clearly state the current execution batch (e.g., "Current batch: Steps 1.1-1.3") and where we are in the overall plan
- After completing a batch, stop and get explicit approval before proceeding to the next batch
- Each batch should be a coherent, testable unit of work — never leave the codebase in a broken state between batches
- If something goes sideways, STOP and re-plan immediately — don't keep pushing

## Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- One task per subagent for focused execution

## Demand Elegance
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky, step back and implement the clean solution
- Skip this for simple, obvious fixes — don't over-engineer

## Verification & Quality Gate
- Never mark a task complete without proving it works
- After making changes, always verify by running the project's test command
- If no tests exist for changed code, write them
- For Python: prefer pytest. Run with `pytest -x -q` for fast feedback
- Check types with `mypy` or `pyright` if configured in the project
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"

## Autonomous Bug Fixing
- When given a bug report: just fix it — don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them
- Zero context switching required from the user
- Go fix failing CI tests without being told how

## Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Review lessons at session start for relevant project

## Git Workflow
- Always work on a feature branch — never commit directly to main
- Branch naming: `feature/`, `fix/`, `chore/` prefixes
- Commit messages: imperative mood, concise first line (<72 chars), body if non-obvious
- Always run tests and linting before committing
- One logical change per commit; squash WIP commits before PR
- Break work into meaningful commits that others can review (one commit per logical step/feature, not one giant commit)
- Push the branch and cut a PR when a batch is complete so the team can track progress

## How to Work
- Read the project's CLAUDE.md first — it overrides anything here
- Before implementing non-trivial changes, outline the plan and wait for confirmation
- When unsure about project structure, search the codebase before guessing
- For complex domain logic or unfamiliar libraries, read `docs/` or relevant project markdown files before coding
- Never modify config files (.env, secrets, CI configs) without explicit confirmation
- Prefer editing existing files over creating new ones unless the change clearly warrants a new module

## What NOT to Do
- Don't add dependencies without asking
- Don't refactor code unrelated to the current task
- Don't generate boilerplate comments or docstrings that just restate the function name
- Never write secrets, credentials, PII, or sensitive data to any file, output, or commit — not even to private repos. If in doubt, ask
