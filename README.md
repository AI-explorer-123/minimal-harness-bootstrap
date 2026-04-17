# minimal-harness-bootstrap

Reusable Codex skill for adding a lightweight agent-ready harness to an existing repository.

It focuses on three concrete outputs:

- a concise top-level `AGENTS.md`
- practical repository docs under `docs/`
- a repeatable smoke-test entrypoint

## Skill Files

The Codex-relevant files live at the repository root:

- `SKILL.md`
- `agents/openai.yaml`

`README.md` is only for GitHub visitors. Codex reads `SKILL.md`.

## Install

Clone this repository into your local Codex skills directory:

```bash
git clone https://github.com/AI-explorer-123/minimal-harness-bootstrap.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/minimal-harness-bootstrap"
```

If you already have the repo locally, copy or symlink the repository root into `${CODEX_HOME:-$HOME/.codex}/skills/minimal-harness-bootstrap`.

## Example

```text
Use $minimal-harness-bootstrap to add AGENTS.md, practical docs, and smoke tests to a repository.
```
