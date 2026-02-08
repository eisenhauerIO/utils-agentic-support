# Project Memory - ChernyCode

This repository contains configurations and workflows inspired by Boris Cherny's Claude Code tips.

## Project Purpose

This project serves as a template and reference implementation for optimizing AI-assisted coding workflows with Claude Code and Cursor. It contains:
- Memory files (CLAUDE.md, AGENTS.md)
- Custom skills and commands
- Cursor rules
- Subagent configurations

## Coding Standards

### Python
- **Version**: Python 3.10+
- **Formatter**: Ruff (replaces black, isort, flake8)
- **Testing**: pytest with 80%+ coverage
- **Type hints**: Required for all functions
- **Docstrings**: Google-style
- **Naming**: snake_case for functions/variables, PascalCase for classes

### General
- Indentation: 4 spaces
- Max line length: 120 characters
- Error handling: Try-except with logging
- Use structured logging with `structlog`

## Common Workflows

### Git Workflow
- Follow GitHub Flow (feature branches from main)
- Use Conventional Commits format:
  - `feat:` new feature
  - `fix:` bug fix
  - `docs:` documentation
  - `refactor:` code refactoring
  - `test:` adding tests
  - `chore:` maintenance

### Testing
- Run tests with: `pytest`
- Run with coverage: `pytest --cov`
- Always run tests before committing

### Code Quality
- Format code: `ruff format .`
- Lint code: `ruff check .`
- Fix linting issues: `ruff check --fix .`

## Key Files

- `CLAUDE.md` - This file, Claude Code memory
- `AGENTS.md` - Cursor agent instructions
- `.cursor/skills/` - Modular Cursor skills
- `threads.md` - Source material from Boris Cherny

## Known Pitfalls

<!-- Add corrections here as you encounter issues -->
<!-- Example: "When creating pytest fixtures, always use scope='function' unless shared state is explicitly needed" -->

## Verification

Before completing any task:
1. Run the test suite if tests exist
2. Run linter to check for issues
3. Verify changes work as expected

---
*Update this file whenever Claude makes a mistake: "Update CLAUDE.md so you don't make that mistake again"*
