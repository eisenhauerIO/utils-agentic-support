---
name: add-feature
description: Scaffold a new feature following project-specific patterns. Reads feature-type instructions from .claude/skills/feature-types/ to handle different feature types (e.g., model, transform).
argument-hint: [feature-type] [feature-name-in-snake-case]
allowed-tools: Read, Grep, Write, Edit, Bash, Glob
---

# Add Feature

You are scaffolding a new feature. This skill follows a standard workflow and delegates feature-type-specific details to a project-specific instruction file.

## Step 0: Parse arguments

The user provides: `{feature_type} {feature_name}`

- `FEATURE_TYPE`: The kind of feature to scaffold (e.g., `model`, `transform`)
- `FEATURE_NAME`: The snake_case name (e.g., `difference_in_differences`)

If only one argument is provided, treat it as `FEATURE_NAME` and ask the user for the `FEATURE_TYPE`.

## Step 1: Load feature-type instructions

Read the feature-type instruction file at:

```
.claude/skills/feature-types/{FEATURE_TYPE}.md
```

If the file does not exist, inform the user that no instructions are available for feature type `{FEATURE_TYPE}` and list the available feature types by checking which `.md` files exist in `.claude/skills/feature-types/`. Then stop.

The feature-type file defines these sections (all optional — skip any that are absent):

| Section | Purpose |
|---|---|
| `## Naming` | How to derive class names, directory paths, registry keys, etc. from `FEATURE_NAME` |
| `## Requirements` | Questions to ask the user before writing code |
| `## References` | Files to read for style and pattern matching |
| `## Plan` | What the implementation plan should cover |
| `## Implementation` | Specific files to create and modify |
| `## Verification` | Feature-type-specific checklist items |

Follow all instructions from the feature-type file within the workflow stages below.

## Step 2: Derive naming conventions

Follow the `## Naming` section from the feature-type file to derive all names, paths, and keys from `FEATURE_NAME`.

## Step 3: Gather requirements from the user

Follow the `## Requirements` section from the feature-type file. Use a two-phase approach:

**Phase A — Overview.** Print all questions at once so the user can see the full scope.

**Phase B — Walk through one by one.** Ask each question individually using AskUserQuestion, waiting for the answer before moving to the next.

## Step 4: Read reference files

Before writing any code, read all files listed in the `## References` section of the feature-type file. Match their exact code style and patterns.

Also read `DESIGN-PHILOSOPHY.md` in the project root if it exists.

## Step 5: Write a plan

Before writing any code, present an implementation plan to the user. Include:

1. **Files to create/modify** — every file path
2. **Design summary** — what the key components will do
3. **Data flow** — how data moves through the new feature
4. **Key decisions** — any non-obvious choices

Also include anything specified in the `## Plan` section of the feature-type file.

Wait for user approval before proceeding.

## Step 6: Implement

Follow the `## Implementation` section from the feature-type file. Create all specified files and make all specified modifications.

## Step 7: Create a feature branch

All work must be done on a feature branch, not on `main`.

```bash
git checkout -b add-{FEATURE_TYPE}-{FEATURE_NAME}
```

Commit all new and modified files with a descriptive message:
```bash
git commit -m "Add {FEATURE_NAME} {FEATURE_TYPE}"
```

## Step 8: Run tests and lint

Run feature-specific tests first, then the full test suite, then the linter. Use the project's configured test/lint commands (e.g., `hatch run test`, `hatch run lint`).

Fix any failures before proceeding.

## Step 9: Push and create a pull request

Push the branch and create a PR targeting `main`:

```bash
git push -u origin add-{FEATURE_TYPE}-{FEATURE_NAME}
gh pr create --title "Add {FEATURE_NAME} {FEATURE_TYPE}" --body "$(cat <<'EOF'
## Summary
- New {FEATURE_TYPE}: `{FEATURE_NAME}`
- {Brief description from the plan}

## Test plan
- [ ] Feature-specific tests pass
- [ ] Full test suite passes
- [ ] Lint passes
- [ ] CI passes

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

## Step 10: Verify CI

After creating the PR, wait for CI and check the result:

```bash
gh pr checks --watch
```

If CI fails, fix the issues, commit, push, and re-check. Do not consider the task complete until CI is green.

## Step 11: Final verification

Run through the `## Verification` section from the feature-type file. Confirm every item passes before declaring done.
