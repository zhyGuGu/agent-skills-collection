# Contributing

Thanks for your interest in contributing to this agent skills collection.

## Repo layout

- Skills live under `skills/<skill-name>/`.
- Each skill must include `skills/<skill-name>/SKILL.md`.

## Add a new skill

1. Pick a skill name that follows the rules in "Skill naming rules".
2. Create the directory: `skills/<skill-name>/`.
3. Add `skills/<skill-name>/SKILL.md`.
4. Run validation (see "Validation").

## Skill naming rules

`<skill-name>` must:

- Be 1-64 characters.
- Use only lowercase letters (`a-z`), digits (`0-9`), and hyphens (`-`).
- Not start or end with a hyphen.
- Not contain `--` (no consecutive hyphens).

Examples:

- Good: `accessibility-audit`, `terraform-patterns`, `mlops-101`
- Bad: `MySkill`, `-leading`, `trailing-`, `double--dash`

## SKILL.md format

`skills/<skill-name>/SKILL.md` is Markdown with a YAML frontmatter block at the top:

```yaml
---
name: my-skill-name
description: Short, specific description of the skill.
license: MIT
allowed-tools: bash
metadata:
  tags: example
compatibility: ">=0.1"
---
```

### Frontmatter allowed keys

Only these keys are allowed in frontmatter:

- `name`
- `description`
- `license`
- `allowed-tools`
- `metadata`
- `compatibility`

Notes:

- Keep `name` in sync with the directory name: `skills/<name>/SKILL.md`.
- `allowed-tools` must be a string.
- `compatibility` must be a string.
- `metadata` values must be strings.

## Validation

We plan to run this in CI:

```bash
agentskills validate skills/<skill-name>
agentskills validate skills/
```

This is a Python-based validator; run it locally before opening a PR.

## Pull request workflow (no gh CLI)

1. Fork the repo on GitHub.
2. Clone your fork:

```bash
git clone https://github.com/yourusername/agent-skills-collection.git
cd agent-skills-collection
```

3. Create a branch:

```bash
git checkout -b skill/<skill-name>
```

4. Make changes and commit:

```bash
git add skills/<skill-name>/SKILL.md
git commit -m "docs(skill): add <skill-name>"
```

5. Push to your fork:

```bash
git push origin skill/<skill-name>
```

6. Open a pull request using the GitHub web interface.
