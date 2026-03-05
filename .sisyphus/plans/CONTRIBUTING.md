# Contributing to Agent Skills Collection

Thank you for your interest in contributing! This document provides guidelines for creating new skills and improving existing ones.

## 🎯 Contribution Types

### 1. New Skills
- Identify underserved niches
- Follow the skill template
- Include comprehensive documentation
- Provide working examples

### 2. Skill Improvements
- Fix errors or inaccuracies
- Add missing content
- Update for new framework versions
- Improve explanations

### 3. Bug Reports
- Report incorrect information
- Identify broken examples
- Flag outdated practices

### 4. Documentation
- Improve README files
- Add usage examples
- Create video tutorials
- Translate content

---

## 🚀 Quick Start

### Prerequisites
- GitHub account
- Git installed locally
- Familiarity with Markdown
- Knowledge of your skill domain

### Setting Up

1. **Fork the repository**
   ```bash
   git clone https://github.com/yourusername/agent-skills-collection.git
   cd agent-skills-collection
   ```

2. **Create a branch**
   ```bash
   git checkout -b skill/my-new-skill
   ```

3. **Create your skill** following the template

4. **Test your skill** with Claude Code or OpenCode

5. **Submit a PR**

---

## 📋 Skill Development Guide

### Step 1: Research

Before creating a skill:
- [ ] Check skills.sh for existing similar skills
- [ ] Identify the gap you're filling
- [ ] Define your target audience
- [ ] List key capabilities

### Step 2: Planning

Create a planning document:
```markdown
## Skill: [Name]

### Problem Statement
[What problem does this solve?]

### Target Users
[Who will use this?]

### Key Features
- Feature 1
- Feature 2
- Feature 3

### Content Outline
1. Section 1
2. Section 2
3. Section 3

### Examples Needed
- Example 1
- Example 2
```

### Step 3: Structure

Create the skill directory:
```
my-skill/
├── README.md              # Public-facing description
├── SKILL.md               # Main skill file (REQUIRED)
├── guide-1.md             # Supporting guides
├── guide-2.md
├── examples/              # Code examples
│   ├── example-1.md
│   └── example-2.md
└── resources/             # Additional resources
    └── reference.md
```

### Step 4: SKILL.md Template

```yaml
---
name: my-skill-name
description: Clear, concise description of what this skill does (100-200 chars)
version: 1.0.0
author: yourusername
tags: [tag1, tag2, tag3]
---

# My Skill Name

## When to Use
[List 5-10 trigger conditions when this skill should be activated]

## Capabilities
[Numbered list of 5-10 specific capabilities]

## Quick Start
[2-3 sentence quickstart guide]

## Main Content
[Organized sections covering all capabilities]

### Subsection 1
[Detailed content]

### Subsection 2
[Detailed content]

## Examples

### Example 1: [Use Case]
```[language]
[Code example]
```

### Example 2: [Use Case]
```[language]
[Code example]
```

## Best Practices
[Do's and don'ts]

## Common Mistakes
[What to avoid]

## Resources
[Links to official docs, further reading]
```

### Step 5: Content Guidelines

#### Writing Style
- **Clear**: Use simple language, avoid jargon
- **Concise**: Get to the point quickly
- **Actionable**: Provide concrete steps
- **Complete**: Cover edge cases and gotchas

#### Code Examples
- Must be tested and working
- Include comments
- Show both "before" and "after" where relevant
- Cover multiple frameworks if applicable

#### Formatting
- Use proper Markdown
- Include YAML frontmatter
- Use consistent heading levels
- Include code block language tags

---

## ✅ Quality Checklist

Before submitting a PR:

### Content Quality
- [ ] No spelling or grammar errors
- [ ] All code examples are tested
- [ ] Information is accurate and current
- [ ] Edge cases are covered
- [ ] Examples are practical

### Structure Quality
- [ ] SKILL.md follows the template
- [ ] YAML frontmatter is complete
- [ ] Sections are logically organized
- [ ] Table of contents is included
- [ ] Internal links work

### Completeness
- [ ] All claimed capabilities are documented
- [ ] At least 5 code examples
- [ ] Troubleshooting section included
- [ ] Resources section included
- [ ] README.md is complete

### Testing
- [ ] Tested with Claude Code
- [ ] Tested with OpenCode
- [ ] All examples produce expected results
- [ ] No broken links

---

## 📊 Skill Evaluation Criteria

Skills are evaluated on:

| Criteria | Weight | Description |
|----------|--------|-------------|
| **Utility** | 30% | Solves a real problem |
| **Completeness** | 25% | Comprehensive coverage |
| **Accuracy** | 20% | Correct information |
| **Clarity** | 15% | Easy to understand |
| **Examples** | 10% | Practical code samples |

**Minimum passing score**: 75/100

---

## 🔍 Review Process

### 1. Automated Checks
- YAML validation
- Link checking
- Markdown linting
- Spell checking

### 2. Community Review
- Anyone can review
- Constructive feedback encouraged
- Discussion for improvements

### 3. Maintainer Review
- Final approval
- Quality verification
- Merge decision

### Timeline
- Automated checks: Immediate
- Community review: 3-7 days
- Maintainer review: 1-3 days

---

## 🏆 Recognition

### Contributor Levels

**🌱 Seed Contributor**
- 1-2 merged PRs
- Listed in CONTRIBUTORS.md

**🌿 Growth Contributor**
- 3-5 merged PRs
- Skill co-author credit
- Twitter shoutout

**🌳 Core Contributor**
- 5+ merged PRs
- Maintainer status
- Decision-making privileges
- Conference talk opportunity

### Badges
Earn badges for:
- 🏅 First Skill
- 🎨 Design Excellence
- 📚 Documentation Master
- 🐛 Bug Hunter
- 🚀 Innovation Award

---

## 🐛 Reporting Issues

### Bug Reports
Use this template:
```markdown
**Skill**: [Name]
**Section**: [Where the issue is]

**Current**: [What's wrong]
**Expected**: [What it should be]

**Steps to Reproduce**:
1. Step 1
2. Step 2
3. Step 3

**Additional Context**:
[Any other relevant info]
```

### Feature Requests
```markdown
**Skill**: [Name or "New Skill"]

**Problem**: [What problem does this solve?]

**Proposed Solution**: [How should it work?]

**Alternatives**: [Other approaches considered]

**Additional Context**:
[Any supporting info]
```

---

## 📚 Resources

### Skill Development
- [Skill Template](templates/skill-template.md)
- [Example Skills](examples/)
- [Writing Guide](docs/writing-guide.md)
- [Markdown Reference](docs/markdown-reference.md)

### Testing
- [Testing Guide](docs/testing-guide.md)
- [Claude Code Setup](docs/claude-code-setup.md)
- [OpenCode Setup](docs/opencode-setup.md)

### Community
- [Discord Server](https://discord.gg/yourserver)
- [Discussions](https://github.com/yourusername/agent-skills-collection/discussions)
- [Office Hours](https://calendly.com/yourname/office-hours)

---

## ⚖️ Code of Conduct

### Our Standards
- Be respectful and inclusive
- Welcome newcomers
- Provide constructive feedback
- Focus on what's best for the community

### Unacceptable Behavior
- Harassment or discrimination
- Trolling or insulting comments
- Personal attacks
- Publishing private information

### Enforcement
Violations may result in:
1. Warning
2. Temporary ban
3. Permanent ban

Report violations to [email@example.com](mailto:email@example.com)

---

## 🎓 Learning Path

### Beginner
1. Read existing skills
2. Fix typos or broken links
3. Add examples to existing skills
4. Create a simple new skill

### Intermediate
1. Create comprehensive skills
2. Review others' PRs
3. Improve skill templates
4. Write documentation

### Advanced
1. Maintain multiple skills
2. Mentor new contributors
3. Design skill architecture
4. Lead working groups

---

## 📝 Commit Message Guidelines

Use conventional commits:

```
type(scope): subject

body (optional)

footer (optional)
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `test`: Tests
- `chore`: Maintenance

**Examples**:
```
feat(accessibility): add keyboard navigation patterns

docs(terraform): update AWS provider examples

fix(data-science): correct sklearn pipeline example
```

---

## 🔐 Security

### Reporting Vulnerabilities
- Email: security@example.com
- Do not create public issues
- Provide detailed reproduction steps
- Allow 30 days before disclosure

### Security Best Practices
- No secrets in examples
- No malicious code
- Review dependencies
- Follow OWASP guidelines

---

## 💬 Communication Channels

### GitHub
- Issues: Bug reports, feature requests
- Discussions: General questions, ideas
- PRs: Code contributions

### Real-time
- Discord: [Join here](https://discord.gg/yourserver)
- Twitter: [@yourusername](https://twitter.com/yourusername)

### Email
- General: hello@example.com
- Security: security@example.com
- Business: business@example.com

---

## 🎯 Quick Reference

| Task | Command |
|------|---------|
| Create branch | `git checkout -b skill/name` |
| Check status | `git status` |
| Stage changes | `git add .` |
| Commit | `git commit -m "feat: description"` |
| Push | `git push origin branch-name` |
| Create PR | GitHub web interface |

---

## ❓ FAQ

**Q: Do I need to be an expert?**  
A: No! Domain knowledge helps, but clear writing and good examples matter more.

**Q: Can I submit a partial skill?**  
A: Yes, mark it as [WIP] in the PR title. We'll help you complete it.

**Q: How long does review take?**  
A: Usually 3-7 days for community review, 1-3 days for maintainer review.

**Q: Can I update someone else's skill?**  
A: Yes! Submit a PR with improvements. Original authors are credited.

**Q: What if my skill idea exists?**  
A: Check if yours offers something different. If similar, consider contributing to the existing one.

**Q: Do skills need code?**  
A: No, skills can be purely informational (best practices, workflows, etc.)

---

## 🙏 Thank You!

Every contribution, no matter how small, makes this project better. Thank you for helping build the future of AI agent capabilities!

---

<p align="center">
  <b>Happy Contributing! 🚀</b>
</p>
