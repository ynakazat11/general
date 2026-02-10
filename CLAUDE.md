# Global Preferences

## Identity
- I work primarily in Python (FastAPI, Flask, scripting, ML/AI tooling)
- I use Neovim as my editor and zsh as my shell
- I maintain projects on GitHub

## Code Quality
- Prefer simple, readable code over clever abstractions
- Type hints required on all function signatures
- Use dataclasses or Pydantic models over raw dicts for structured data
- Prefer composition over inheritance
- Small functions that do one thing; if a function needs a comment explaining "what", it's too complex
- Handle errors explicitly — no bare `except:`, no silent failures

## Execution Strategy
- For multi-step plans, implement in small batches (2-4 steps per batch)
- In plan mode, the plan header must clearly state the current execution batch (e.g., "Current batch: Steps 1.1-1.3") and where we are in the overall plan
- After completing a batch, stop and get explicit approval before proceeding to the next batch
- Each batch should be a coherent, testable unit of work — never leave the codebase in a broken state between batches

## Git Workflow
- Always work on a feature branch — never commit directly to main
- Branch naming: `feature/`, `fix/`, `chore/` prefixes
- Commit messages: imperative mood, concise first line (<72 chars), body if non-obvious
- Always run tests and linting before committing
- One logical change per commit; squash WIP commits before PR
- Break work into meaningful commits that others can review (one commit per logical step/feature, not one giant commit)
- Push the branch and cut a PR when a batch is complete so the team can track progress

## Testing & Verification
- After making changes, always verify by running the project's test command
- If no tests exist for changed code, write them
- For Python: prefer pytest. Run with `pytest -x -q` for fast feedback
- Check types with `mypy` or `pyright` if configured in the project

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
- Don't use `os.system()` — use `subprocess.run()` with proper error handling
- Never write secrets, credentials, PII, or sensitive data to any file, output, or commit — not even to private repos. If in doubt, ask
