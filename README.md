# minimal-harness-bootstrap

Reusable Codex skill for adding a lightweight harness to an existing repository.

It focuses on three concrete outputs:

- a concise top-level `AGENTS.md`
- practical repository docs under `docs/`
- a repeatable smoke-test entrypoint

The skill is intentionally narrow. It does not try to redesign CI, feature tracking, or broader agent orchestration unless asked.

## Repository Layout

- `minimal-harness-bootstrap/SKILL.md`: skill instructions
- `minimal-harness-bootstrap/agents/openai.yaml`: UI metadata

## Install

Copy or symlink the `minimal-harness-bootstrap/` folder into your Codex skills directory, typically:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R minimal-harness-bootstrap "${CODEX_HOME:-$HOME/.codex}/skills/"
```

## Example

```text
Use $minimal-harness-bootstrap to add AGENTS.md, practical docs, and smoke tests to a repository.
```
