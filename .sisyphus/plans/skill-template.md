# Skill Template

Use this template as a starting point for creating new agent skills.

## Quick Start

1. Copy this template to `your-skill/SKILL.md`
2. Replace placeholder content
3. Add supporting files
4. Test with Claude Code or OpenCode
5. Submit PR

---

## SKILL.md Template

```markdown
---
name: your-skill-name
description: A clear, compelling description of what this skill does (100-200 characters). Focus on the value proposition and when to use it.
version: 1.0.0
author: your-github-username
tags: [relevant, tags, here]
---

# [Skill Name]

[Brief 2-3 sentence overview of the skill and its main value proposition]

## When to Use

This skill is triggered when users:

1. [Specific scenario 1 - be concrete]
2. [Specific scenario 2 - be concrete]
3. [Specific scenario 3 - be concrete]
4. [Specific scenario 4 - be concrete]
5. [Specific scenario 5 - be concrete]

**Keywords**: [List 10-15 keywords that should trigger this skill]

## Capabilities

This skill provides:

1. **[Capability 1]**: [Brief description]
2. **[Capability 2]**: [Brief description]
3. **[Capability 3]**: [Brief description]
4. **[Capability 4]**: [Brief description]
5. **[Capability 5]**: [Brief description]

## Quick Start

[2-3 sentences on how to get started quickly. Include a simple example.]

Example:
\`\`\`bash
# Quick command or code example
npx your-tool do-something
\`\`\`

## Core Concepts

[Explain the fundamental concepts users need to understand]

### [Concept 1]
[Explanation]

### [Concept 2]
[Explanation]

### [Concept 3]
[Explanation]

## Main Workflow

[Describe the primary workflow or process this skill guides]

### Step 1: [Action]
[Detailed instructions]

### Step 2: [Action]
[Detailed instructions]

### Step 3: [Action]
[Detailed instructions]

## Examples

### Example 1: [Common Use Case]

**Scenario**: [Describe the situation]

**Input**:
\`\`\`[language]
[Code or input example]
\`\`\`

**Process**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Output**:
\`\`\`[language]
[Result]
\`\`\`

### Example 2: [Another Use Case]

[Same structure as Example 1]

### Example 3: [Edge Case]

[Same structure, showing how to handle complex scenarios]

## Common Patterns

### Pattern 1: [Pattern Name]

[Description of when to use this pattern]

\`\`\`[language]
[Code example]
\`\`\`

**Best for**: [When to use]
**Avoid when**: [When not to use]

### Pattern 2: [Pattern Name]

[Same structure]

### Pattern 3: [Pattern Name]

[Same structure]

## Decision Framework

[Help users choose between options]

### Decision Matrix

| Scenario | Option A | Option B | Option C |
|----------|----------|----------|----------|
| [Condition 1] | ✅ | ❌ | ✅ |
| [Condition 2] | ❌ | ✅ | ✅ |
| [Condition 3] | ✅ | ✅ | ❌ |

### Questions to Ask

1. **[Question 1]**?
   - If yes → [Recommendation]
   - If no → [Alternative]

2. **[Question 2]**?
   - If yes → [Recommendation]
   - If no → [Alternative]

## Best Practices

### Do's ✅

- [Best practice 1 with explanation]
- [Best practice 2 with explanation]
- [Best practice 3 with explanation]
- [Best practice 4 with explanation]
- [Best practice 5 with explanation]

### Don'ts ❌

- [Anti-pattern 1 with explanation]
- [Anti-pattern 2 with explanation]
- [Anti-pattern 3 with explanation]
- [Anti-pattern 4 with explanation]
- [Anti-pattern 5 with explanation]

## Common Mistakes

### Mistake 1: [Name]

**Problem**: [What goes wrong]

**Impact**: [Why it's bad]

**Solution**: [How to fix it]

\`\`\`[language]
// ❌ Incorrect
[bad code]

// ✅ Correct
[good code]
\`\`\`

### Mistake 2: [Name]

[Same structure]

## Troubleshooting

### Issue: [Problem Description]

**Symptoms**: [What users see]

**Cause**: [Why it happens]

**Solution**: [How to fix]

### Issue: [Problem Description]

[Same structure]

## Advanced Usage

### [Advanced Topic 1]

[Detailed explanation for power users]

### [Advanced Topic 2]

[Detailed explanation]

## Integration

### With [Tool/Framework 1]

[How to integrate with other tools]

### With [Tool/Framework 2]

[How to integrate]

## Performance Considerations

### Optimization Tips

1. [Tip 1 with explanation]
2. [Tip 2 with explanation]
3. [Tip 3 with explanation]

### Benchmarks

| Scenario | Metric | Value |
|----------|--------|-------|
| [Case 1] | [Metric] | [Value] |
| [Case 2] | [Metric] | [Value] |

## Security Considerations

### [Security Topic 1]

[Security guidance]

### [Security Topic 2]

[Security guidance]

## Resources

### Official Documentation
- [Resource 1](link) - [Description]
- [Resource 2](link) - [Description]

### Further Reading
- [Article 1](link) - [Description]
- [Article 2](link) - [Description]

### Tools
- [Tool 1](link) - [Description]
- [Tool 2](link) - [Description]

### Community
- [Forum/Discord](link)
- [Stack Overflow tag](link)

## Changelog

### v1.0.0 (YYYY-MM-DD)
- Initial release
- [Feature 1]
- [Feature 2]

## Contributing

[How to contribute to this skill]

## License

[License information]

## Credits

- [Contributor 1](link) - [Contribution]
- [Contributor 2](link) - [Contribution]
```

---

## Additional Files to Create

### README.md

```markdown
# [Skill Name]

[Brief description]

## Installation

\`\`\`bash
npx skills add yourusername/skill-name
\`\`\`

## Usage

[Brief usage guide]

## Features

- Feature 1
- Feature 2
- Feature 3

## Documentation

Full documentation is in [SKILL.md](./SKILL.md)

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md)

## License

Apache 2.0
```

### examples/

Create a directory with practical examples:

```
examples/
├── basic-example.md
├── advanced-example.md
├── real-world-case-study.md
└── framework-specific/
    ├── react-example.md
    ├── vue-example.md
    └── vanilla-example.md
```

Each example should be a complete, working demonstration.

### resources/

Additional reference materials:

```
resources/
├── glossary.md          # Domain-specific terms
├── cheatsheet.md        # Quick reference
├── faq.md              # Common questions
└── external-links.md   # Curated resources
```

---

## Content Guidelines

### Writing Style

1. **Be Clear**: Use simple language. Avoid jargon unless necessary.
2. **Be Concise**: Get to the point. Remove fluff.
3. **Be Concrete**: Use real examples, not abstract concepts.
4. **Be Complete**: Cover edge cases and common mistakes.
5. **Be Current**: Use up-to-date practices and versions.

### Code Examples

1. **Test Everything**: All code must work.
2. **Comment Liberally**: Explain why, not just what.
3. **Show Context**: Include imports, setup, etc.
4. **Progressive Complexity**: Start simple, build up.
5. **Multiple Languages**: Cover popular frameworks.

### Structure

1. **Logical Flow**: Organize from simple to complex.
2. **Clear Headings**: Use descriptive headers.
3. **Consistent Formatting**: Follow Markdown conventions.
4. **Visual Breaks**: Use lists, tables, code blocks.
5. **Navigable**: Easy to scan and find information.

---

## Quality Checklist

Before submitting:

### Content
- [ ] All claims are accurate
- [ ] All code is tested
- [ ] Examples are practical
- [ ] Edge cases are covered
- [ ] Common mistakes are addressed

### Structure
- [ ] YAML frontmatter is complete
- [ ] All sections are filled
- [ ] Examples have all 3 parts (Scenario, Input, Output)
- [ ] Decision frameworks are clear
- [ ] Resources are linked and working

### Style
- [ ] No spelling/grammar errors
- [ ] Consistent terminology
- [ ] Clear headings
- [ ] Proper code formatting
- [ ] Helpful comments

### Testing
- [ ] Tested with Claude Code
- [ ] Tested with OpenCode
- [ ] All links work
- [ ] Examples produce correct output

---

## Examples of Great Skills

Study these for inspiration:

1. **frontend-design** (anthropics/skills) - Comprehensive coverage
2. **mcp-builder** (anthropics/skills) - Clear examples
3. **systematic-debugging** (obra/superpowers) - Great structure
4. **webapp-testing** (anthropics/skills) - Practical workflows

---

## Tips for Success

1. **Start Small**: Build MVP, then expand
2. **Get Feedback**: Share drafts early
3. **Iterate**: Improve based on usage
4. **Stay Current**: Update for new versions
5. **Engage Community**: Respond to issues

---

## Questions?

- Review existing skills in this repo
- Check [CONTRIBUTING.md](../CONTRIBUTING.md)
- Open a Discussion for help

Happy skill building! 🚀
