# agent-skills-collection

A small collection of agent skills (skills.sh format) focused on niches that are usually underserved.

## Skills

- `skills/accessibility-audit` - Web accessibility auditing guidance (WCAG-oriented checks and remediation ideas).
- `skills/data-science-patterns` - Repeatable data science / ML workflow patterns.
- `skills/terraform-patterns` - Terraform/IaC architecture and workflow patterns.
- `skills/flutter-best-practices` - Flutter engineering best practices and decision guides.
- `skills/audio-production` - Audio production and editing workflows for creators.
- `skills/design-tokens-migration` - A migration playbook for introducing design tokens into an existing UI codebase.
- `skills/event-instrumentation-spec` - Privacy-aware analytics tracking plan templates and QA checklists.
- `skills/data-retention-privacy-audit` - Practical data mapping and retention/deletion planning templates.
- `skills/staged-rollout-playbook` - Progressive delivery checklists with health metrics and rollback triggers.
- `skills/incident-postmortem-facilitator` - Blameless postmortem facilitation templates and action item rubric.

## Install

Install the whole collection:

```bash
npx skills add zhyGuGu/agent-skills-collection
```

Or install a single skill by URL:

```bash
npx skills add https://github.com/zhyGuGu/agent-skills-collection/tree/main/skills/accessibility-audit
```

## Contributing / Local Development

- Repo layout: skills live under `skills/<skill-name>/`.
- Each skill typically provides `skills/<skill-name>/SKILL.md` (common convention on skills.sh).

## Publishing Notes

- The `gh` CLI is not installed in this environment.
- GitHub repo/org creation and pushing are manual (e.g., create repo on GitHub, add a git remote, then `git push`).
