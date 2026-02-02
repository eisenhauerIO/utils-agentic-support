# utils-agentic-support

Unified AI development support for eisenhauerIO projects. Contains both human-readable
standards and machine-executable runtime configurations for Claude Code.

## Directory Structure

```
utils-agentic-support/
├── standards/          # Human-readable guidelines
│   ├── writing/        # Prose and communication style
│   ├── coding/         # Code style and conventions
│   ├── documentation/  # How to document code and decisions
│   └── research/       # Academic and analytical standards
├── runtime/            # Machine-executable configurations
│   ├── memory/         # CLAUDE.md, AGENTS.md templates
│   ├── skills/         # Slash command workflows
│   └── subagents/      # Specialized task runners
├── templates/          # Project bootstrapping files
└── cursor/             # Cursor-specific configs (reference)
```

---

## `standards/` — Human-Readable Guidelines

Static documentation that defines HOW we work. Read by humans and AI for context.
Updated infrequently. Changes require team review.

| Subdirectory | Purpose | Examples |
|--------------|---------|----------|
| `standards/writing/` | Prose and communication style | Tone, structure, clarity rules |
| `standards/coding/` | Code style and conventions | Python patterns, naming, type hints |
| `standards/documentation/` | How to document code and decisions | Docstrings, READMEs, ADRs |
| `standards/research/` | Academic and analytical standards | Citation style, methodology rigor |

**When to add here:** New team convention, style guide update, documentation template.

---

## `runtime/` — Machine-Executable Configurations

Active files that AI tools READ AND EXECUTE during coding sessions.
Updated frequently as workflows improve.

| Subdirectory | Purpose | Triggered By |
|--------------|---------|--------------|
| `runtime/memory/` | Project context AI loads at session start | Automatic on session start |
| `runtime/skills/` | Multi-step workflows | User invokes `/skill-name` |
| `runtime/subagents/` | Specialized task runners | AI spawns as needed |

### `runtime/memory/`

- `CLAUDE.md` — Template for project memory (copy to project root)
- `AGENTS.md` — Agent definitions and capabilities

### `runtime/skills/`

Executable workflows invoked with slash commands.

| Skill | Command | What it does |
|-------|---------|--------------|
| `commit-push-pr/` | `/commit` | Stage, commit, push, open PR |
| `techdebt/` | `/techdebt` | Find and document technical debt |
| `code-simplifier/` | `/simplify` | Reduce complexity in selected code |
| `eisenhauer/causal-review/` | `/causal` | Review for causal inference best practices |
| `eisenhauer/impact-eval/` | `/impact` | Document impact evaluation methodology |

### `runtime/subagents/`

Isolated agents spawned for specific tasks.

| Subagent | Purpose |
|----------|---------|
| `code-reviewer.md` | Deep code review with standards context |
| `test-writer.md` | Generate comprehensive test suites |
| `doc-generator.md` | Create documentation from code |
| `eisenhauer/methodology-checker/` | Validate econometric methodology |

---

## `templates/` — Project Bootstrapping

Starter files for new eisenhauerIO projects.

| Template | Purpose |
|----------|---------|
| `CLAUDE.md.template` | Project memory file starter |

---

## Usage

### Adding to a Project

```bash
# Add as submodule
git submodule add https://github.com/eisenhauerIO/utils-agentic-support.git .agentic

# Copy memory file to project root (customize per project)
cp .agentic/templates/CLAUDE.md.template CLAUDE.md
```

### Project-Specific Customization

Each project should have its own `CLAUDE.md` at the root that:

1. References shared standards: `See .agentic/standards/coding/python.md`
2. Adds project-specific context (architecture, key files, conventions)
3. Imports relevant skills

---

## Key Concepts

### Memory Files (CLAUDE.md)

These files provide persistent context that Claude reads at the start of every session:

- **Project-level** (`./CLAUDE.md`): Shared with your team via git
- **Personal** (`~/.claude/CLAUDE.md`): Your preferences across all projects
- **Local** (`./CLAUDE.local.md`): Personal project settings, gitignored

**Best Practice**: After every correction, say:
> "Update CLAUDE.md so you don't make that mistake again"

### Skills

Skills are reusable workflows you can invoke with `/skill-name`. Create new skills by adding a directory with `SKILL.md` to `runtime/skills/`.

### Subagents

Subagents run specialized tasks in their own context window. They enable parallel execution and context isolation for focused tasks like code review or test generation.

---

## Contributing

- **Standards changes:** Require team discussion and PR review
- **Runtime changes:** Can iterate quickly, test in one project first
- **New skills:** Add to `runtime/skills/eisenhauer/` for domain-specific workflows

---

## Origin

Forked from [ChernyCode](https://github.com/meleantonio/ChernyCode) (Boris Cherny's Claude Code productivity tips).
Developed independently as a strategic asset for eisenhauerIO.

## License

MIT
