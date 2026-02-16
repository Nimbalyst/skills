# Contributing Skills

Guidelines for creating and submitting new skills to this collection.

## Skill Structure

Each skill lives in its own directory under a category folder:

```
skills/[category]/[skill-name]/
  SKILL.md          # Required: The skill definition
  examples/         # Optional: Example outputs
    example-1.md
```

## Creating a New Skill

### 1. Choose a Category

| Category | For |
| --- | --- |
| `dev/` | Developer workflows (git, testing, code review, debugging) |
| `product/` | Product management (PRDs, strategy, triage, status reports) |
| `research/` | Research and analysis (competitive, user research, deep dives) |
| `content/` | Content creation (blogs, docs, slides, marketing) |
| `meta/` | Meta tools (workflow optimization, skill creation) |

### 2. Name Your Skill

- Use `kebab-case`: `branch-reviewer`, `prd-writer`
- Be descriptive but concise
- Name should indicate what the skill does

### 3. Write SKILL.md

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: my-skill-name
description: One sentence describing what this skill does and when Claude should use it.
---
```

**Frontmatter fields:**

| Field | Required | Description |
| --- | --- | --- |
| `name` | Yes | Kebab-case identifier matching the folder name |
| `description` | Yes | Tells Claude when to activate this skill. Be specific about triggers. |

### 4. Write the Skill Body

After the frontmatter, write markdown instructions for Claude. Good skills include:

- **What it does** - Clear explanation of the skill's purpose
- **Process/workflow** - Step-by-step instructions Claude should follow
- **Templates** - Output formats and structure
- **Best practices** - Guidelines for quality output
- **What to ask** - Questions to clarify ambiguous requests

### Description Best Practices

The `description` field is critical -- it tells Claude when to activate the skill. Good descriptions:

- State what the skill does AND when to use it
- Include trigger phrases: "Use when..."
- Are specific enough to avoid false activations

```yaml
# Good
description: Create structured Product Requirements Documents (PRDs) with prioritized requirements. Use when writing product specs, feature requirements, or project briefs.

# Bad - too vague
description: Help with product work.

# Bad - no trigger context
description: Write PRDs.
```

## Quality Checklist

Before submitting:

- [ ] `name` in frontmatter matches the folder name
- [ ] `description` includes both what it does AND when to use it
- [ ] No tool-specific dependencies (no MCP tools, no specific CLI features)
- [ ] No product-specific references (works for any project, not just one product)
- [ ] Templates use placeholder values, not real data
- [ ] Instructions are clear enough for Claude to follow without additional context
- [ ] Markdown renders correctly

## Submitting

1. Fork this repository
2. Create your skill in the appropriate category
3. Test it by installing locally
4. Submit a pull request with a brief description of what the skill does

## Tips

- **Start simple**: A focused skill that does one thing well is better than a bloated skill
- **Be opinionated**: Good skills encode best practices, not just templates
- **Include examples**: If your skill produces structured output, show what good output looks like
- **Test it**: Install the skill and try several prompts to make sure it activates correctly
