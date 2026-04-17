---
name: minimal-harness-bootstrap
description: Add a lightweight agent-ready harness to an existing repository by creating or updating AGENTS.md, practical docs under docs/, and repeatable smoke tests. Use when a repository works for humans but lacks clear agent instructions, lightweight project docs, or a low-cost verification path for quick agent iterations.
---

# Minimal Harness Bootstrap

## Overview

Turn an existing repository into a minimally agent-friendly workspace without trying to solve full harness engineering. Focus on three outputs only: a concise top-level `AGENTS.md`, useful project docs under `docs/`, and a repeatable smoke-test entrypoint.

## Scope Rules

Keep this skill narrow.

- Do create or update:
  - `AGENTS.md`
  - a small `docs/` structure
  - one smoke-test script or command entrypoint
- Do not expand scope into full CI redesign, issue workflows, feature-state trackers, or multi-worktree orchestration unless the user explicitly asks for them.
- Do not write long, generic documentation. Every file should help the next agent start, validate, and continue work.

## Workflow

### 1. Inspect the repository before writing anything

Read only the files needed to discover:

- package/runtime manager and language (`pyproject.toml`, `package.json`, `Cargo.toml`, `go.mod`, `Makefile`)
- existing startup commands (`README.md`, `scripts/`, `examples/`)
- current tests (`tests/`, `vibe_tests/`, `spec/`, `__tests__/`)
- any existing agent instructions (`AGENTS.md`, `CLAUDE.md`, `.github/`, `docs/`)

Prefer extracting the repository's current truth over inventing new conventions.

### 2. Choose the cheapest reliable smoke test

A smoke test should prove the repo is alive with minimal cost.

Choose the lightest option that still validates something real:

1. import/package smoke
2. CLI help or startup smoke
3. one small happy-path unit/integration test
4. one minimal API or UI path if nothing else exists

Good smoke tests:

- finish quickly
- avoid GPU or heavyweight model downloads when possible
- avoid secret-dependent flows when possible
- fail loudly with actionable output
- can be run by an agent without interpretation

If the repository has heavyweight tests, add a new lightweight path instead of pointing smoke to the full suite.

### 3. Write `AGENTS.md` as a navigation file

`AGENTS.md` should be short and operational. It is not the full project manual.

Include:

- what the repository is for in 2-4 lines
- where the main code lives
- how to install or bootstrap the project
- the canonical smoke-test command
- the next heavier verification commands if they exist
- editing guardrails specific to this repo
- pointers to docs under `docs/`

Avoid:

- architecture essays
- repeated README content
- speculative rules not enforced by the repo
- guidance that is likely to rot quickly

### 4. Add practical docs under `docs/`

Create only the docs the repo can maintain.

Default structure:

- `docs/overview.md`: what the project does, important directories, primary entrypoints
- `docs/development.md`: setup, local workflow, verification commands, common pitfalls
- `docs/testing.md`: smoke path, heavier tests, environment-sensitive tests

If the repository already has substantial docs, add only missing pages and link to existing material instead of rewriting it.

Each doc should answer concrete questions:

- Where do I start?
- What command should I run first?
- What is safe to edit?
- How do I know I did not break the repo?

### 5. Normalize the smoke entrypoint

Expose one obvious command, usually through one of:

- `scripts/smoke.sh`
- `make smoke`
- `python -m pytest tests/test_smoke.py -q`
- `npm run smoke`

Prefer a shell script when the repository has inconsistent tooling and the script can wrap the canonical command in one stable entrypoint.

The smoke entrypoint should:

- set strict shell flags if it is a shell script
- `cd` to repo root if needed
- print the command it is about to run when helpful
- return non-zero on failure

### 6. Keep changes easy to review

When possible, separate:

- instruction changes (`AGENTS.md`, `docs/`)
- executable validation changes (`scripts/`, tests)

Do not reformat unrelated files.

## Heuristics For Content

Use these defaults unless the repo clearly suggests something better.

### `AGENTS.md`

Aim for sections like:

- `Repository Map`
- `Setup`
- `Verification`
- `Change Boundaries`
- `Docs`

### `docs/overview.md`

Cover:

- project purpose
- key packages/directories
- entrypoints
- what is lightweight vs heavyweight

### `docs/development.md`

Cover:

- environment assumptions
- install steps
- local commands
- common traps such as optional GPU dependencies, external services, or large downloads

### `docs/testing.md`

Cover:

- smoke command
- what the smoke test proves
- heavier test commands
- known environment requirements

## Writing Style

- Prefer short lists and direct commands.
- Prefer repository-specific language over generic harness theory.
- Explicitly mark environment-sensitive commands.
- If a command is optional or expensive, say so.
- Do not claim validation paths you did not inspect.

## Done Criteria

This skill is complete only when all of the following are true:

- `AGENTS.md` exists and points to the real setup and verification path
- `docs/` contains practical pages that match the repo
- there is one clear smoke-test entrypoint
- the smoke-test command was run or an explicit blocker was recorded
- the docs and `AGENTS.md` mention the same canonical smoke command

## Example Request Shapes

- "Add AGENTS.md and a smoke test to this GitHub repo."
- "Make this repo easier for coding agents to work in."
- "Bootstrap lightweight harness docs for this package."
- "I only want AGENTS.md, docs, and smoke tests for this codebase."
