# agent-skills-collection
简体中文 | [English](README.md)

一个小型的 agent skills（skills.sh 格式）集合，专注于那些通常被忽视的细分领域。

## Getting started

安装整个合集：

```bash
npx skills add zhyGuGu/agent-skills-collection
```

或按 URL 安装单个 skill：

```bash
npx skills add https://github.com/zhyGuGu/agent-skills-collection/tree/main/skills/accessibility-audit
```

## Skills

| Skill | What it helps with |
| --- | --- |
| [accessibility-audit](skills/accessibility-audit/) | Web 无障碍审计（面向 WCAG 的检查与修复建议）。 |
| [data-science-patterns](skills/data-science-patterns/) | 可复用的数据科学 / ML 工作流模式。 |
| [terraform-patterns](skills/terraform-patterns/) | Terraform/IaC 架构与工作流模式。 |
| [flutter-best-practices](skills/flutter-best-practices/) | Flutter 工程最佳实践与决策指南。 |
| [audio-production](skills/audio-production/) | 面向创作者的音频制作与剪辑工作流。 |
| [design-tokens-migration](skills/design-tokens-migration/) | 在现有 UI 代码库中引入 design tokens。 |
| [event-instrumentation-spec](skills/event-instrumentation-spec/) | 注重隐私的埋点/分析跟踪方案与 QA 检查清单。 |
| [data-retention-privacy-audit](skills/data-retention-privacy-audit/) | 数据梳理 + 保留/删除规划模板。 |
| [staged-rollout-playbook](skills/staged-rollout-playbook/) | 渐进式发布检查清单，包含指标与回滚触发条件。 |
| [incident-postmortem-facilitator](skills/incident-postmortem-facilitator/) | 无责复盘主持模板与行动项评估标准。 |

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

参见 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [COMMUNITY.md](COMMUNITY.md)。

## Publishing

参见 [PUBLISHING.md](PUBLISHING.md)。

## Enterprise

参见 [ENTERPRISE.md](ENTERPRISE.md)。

## License

参见 [LICENSE](LICENSE)。
