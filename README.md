# agent-skills-collection
English | [简体中文](README.zh-CN.md)

A small collection of agent skills (skills.sh format) focused on niches that are usually underserved.

## Getting started

Install the whole collection:

```bash
npx skills add zhyGuGu/agent-skills-collection
```

Or install a single skill by URL:

```bash
npx skills add https://github.com/zhyGuGu/agent-skills-collection/tree/main/skills/accessibility-audit
```

## Skills

| Skill | What it helps with |
| --- | --- |
| [accessibility-audit](skills/accessibility-audit/) | Web accessibility audits (WCAG-oriented checks and remediation ideas). |
| [data-science-patterns](skills/data-science-patterns/) | Repeatable data science / ML workflow patterns. |
| [terraform-patterns](skills/terraform-patterns/) | Terraform/IaC architecture and workflow patterns. |
| [flutter-best-practices](skills/flutter-best-practices/) | Flutter engineering best practices and decision guides. |
| [audio-production](skills/audio-production/) | Audio production and editing workflows for creators. |
| [design-tokens-migration](skills/design-tokens-migration/) | Introducing design tokens into an existing UI codebase. |
| [event-instrumentation-spec](skills/event-instrumentation-spec/) | Privacy-aware analytics tracking plans and QA checklists. |
| [data-retention-privacy-audit](skills/data-retention-privacy-audit/) | Data mapping plus retention/deletion planning templates. |
| [staged-rollout-playbook](skills/staged-rollout-playbook/) | Progressive delivery checklists with metrics and rollback triggers. |
| [incident-postmortem-facilitator](skills/incident-postmortem-facilitator/) | Blameless postmortem facilitation templates and action-item rubric. |

## Repository structure

```text
agent-skills-collection/
  skills/
    <skill-name>/
      SKILL.md
  CONTRIBUTING.md
  COMMUNITY.md
  PUBLISHING.md
  ENTERPRISE.md
  LICENSE
  README.md
  README.zh-CN.md
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) and [COMMUNITY.md](COMMUNITY.md).

## Publishing

See [PUBLISHING.md](PUBLISHING.md).

## Enterprise

See [ENTERPRISE.md](ENTERPRISE.md).

## License

See [LICENSE](LICENSE).
