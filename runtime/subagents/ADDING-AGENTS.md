# Adding New Agents

This guide explains how to create new agent files that follow the established conventions.

## File Location

Place agent files in: `runtime/subagents/`

Use kebab-case for filenames: `my-agent-name.md`

## File Structure

### 1. YAML Frontmatter

Every agent file starts with YAML frontmatter:

```yaml
---
name: agent-name
description: Brief one-line description of what the agent does.
model: opus
allowed-tools: Read, Grep, Glob, Bash(specific-command*)
---
```

**Fields:**

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Kebab-case identifier matching the filename |
| `description` | Yes | One-line summary of the agent's purpose |
| `model` | Yes | Model to use: `opus`, `sonnet`, or `haiku` |
| `allowed-tools` | Yes | Comma-separated list of permitted tools |

**Tool Syntax:**

- Basic tools: `Read`, `Write`, `Grep`, `Glob`
- Bash with patterns: `Bash(git diff*)`, `Bash(pytest*)`, `Bash(ruff*)`
- Multiple bash patterns: `Bash(git diff*), Bash(git log*)`

### 2. Main Content

Structure the markdown content as follows:

```markdown
# Agent Name Agent

You are [role description with expertise level].

## [Philosophy/Approach Section]

Core principles and mindset for this agent.

## [Guidelines/Standards Section]

Detailed instructions, checklists, or rules.

## [Examples Section] (if applicable)

Code examples in fenced blocks with language specified.

## Workflow

1. **Step One** - Description
2. **Step Two** - Description
3. **Step Three** - Description

## Usage

Explain what the user provides and what the agent outputs.
```

## Conventions

### Naming
- Filename: `kebab-case.md`
- Frontmatter name: matches filename (without `.md`)
- H1 title: `# {Title Case} Agent`

### Content Style
- Start with a role statement: "You are a..."
- Use H2 (`##`) for major sections
- Use H3 (`###`) for subsections
- Include code examples in fenced blocks with language tags
- End with a `## Usage` section describing input/output

### Model Selection
- `opus`: Complex reasoning, code review, architecture decisions
- `sonnet`: General tasks, documentation, straightforward implementations
- `haiku`: Simple tasks, quick lookups, basic formatting

## Example Agent Template

```markdown
---
name: my-agent
description: Brief description of what this agent does.
model: sonnet
allowed-tools: Read, Grep, Glob
---

# My Agent Agent

You are an expert [role] who [core capability].

## Approach

- Principle one
- Principle two
- Principle three

## Guidelines

### Category One
- Guideline A
- Guideline B

### Category Two
- Guideline C
- Guideline D

## Workflow

1. **Analyze** - Understand the input
2. **Process** - Apply expertise
3. **Output** - Deliver results

## Usage

Provide [input type], and this agent will:
1. First action
2. Second action
3. Final deliverable
```

## Checklist

Before adding a new agent, verify:

- [ ] Filename is kebab-case
- [ ] Frontmatter has all required fields
- [ ] `name` matches filename
- [ ] `allowed-tools` lists only necessary tools
- [ ] Content starts with H1 title ending in "Agent"
- [ ] Role statement begins with "You are..."
- [ ] Sections use H2/H3 hierarchy
- [ ] Includes `## Workflow` section
- [ ] Ends with `## Usage` section
