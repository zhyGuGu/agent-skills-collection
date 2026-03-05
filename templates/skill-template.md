# Skill Template

Use this file as a practical starting point for adding a new skill to this repo.

## Layout

Expected layout:

```text
skills/<skill-name>/SKILL.md
```

Example tree:

```text
skills/
  <skill-name>/
    SKILL.md
```

## Skill Name Rules

`<skill-name>` constraints:

- 1-64 characters
- lowercase letters, digits, and hyphens only: `a-z`, `0-9`, `-`
- no leading or trailing hyphen
- no consecutive hyphens (`--`)

Examples:

- valid: `terraform-patterns`, `audio-production`, `mlops101`
- invalid: `-bad`, `bad-`, `BadCaps`, `two--hyphens`, `with_underscore`

## Frontmatter Rules

`skills/<skill-name>/SKILL.md` MUST start with YAML frontmatter.

Allowed frontmatter keys (only these):

- Required:
  - `name` (string; kebab-case; MUST match the directory name)
  - `description` (string)
- Optional (allowed):
  - `license` (string)
  - `allowed-tools` (string)
  - `metadata` (map of string -> string)
  - `compatibility` (string; keep it short, ~500 chars max)

Notes:

- Keep `description` short and concrete; say when to use the skill.
- `metadata` values MUST be strings (for example, use `tags: "a11y, wcag"`, not a YAML list).
- If you include `allowed-tools`, represent it as a single string (for example: `"bash, read, write"`).

## Minimal SKILL.md Template

Copy this into `skills/<skill-name>/SKILL.md` and fill in the placeholders.

Minimal required frontmatter:

```yaml
---
name: <skill-name>
description: <one-line, concrete description of when to use this skill>
---
```

Full frontmatter (includes optional keys):

```yaml
---
name: <skill-name>
description: <one-line, concrete description of when to use this skill>
license: <SPDX identifier or repo license name>
allowed-tools: "<tool-1>, <tool-2>"
metadata:
  owner: "<team-or-handle>"
  tags: "<tag-1>, <tag-2>"
compatibility: "<1 short sentence about supported platforms/runtimes>"
---
```

Body template:

```markdown
# <Skill Title>

<2-3 sentences: what this skill does and what outcome it helps achieve.>

## When to Use

This skill is triggered when users:

1. <specific scenario>
2. <specific scenario>
3. <specific scenario>

Keywords: <comma-separated keywords users might type>

## Capabilities

This skill provides:

1. <capability>
2. <capability>
3. <capability>

## Quick Start

<Short steps or a tiny example prompt the user can paste.>

## Main Workflow

1. <step>
2. <step>
3. <step>

## Examples

### Example 1: <use case>

Scenario: <what the user wants>

Input:

```text
<example input>
```

Output:

```text
<example output>
```
```

## Practical Trim Guide

If you want to keep the skill short, keep only:

- Overview + When to Use + Capabilities
- One Quick Start
- One workflow
- 1-2 examples
