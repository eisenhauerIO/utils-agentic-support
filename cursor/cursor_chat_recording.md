# Cursor Chat Recording

## Session: 2026-02-01

### Topic: Converting Skills to Subagents

**User Request:** The `@cursor_subagents/` folder seems to contain skills rather than subagent definitions. Use the Browser to find Cursor docs for subagents, and use this information to make sure you create these definitions correctly.

**Actions Taken:**

1. **Browsed Cursor Documentation** - Navigated to https://cursor.com/docs/context/subagents to understand the correct format for subagent definitions.

2. **Key Findings from Documentation:**
   - **Location**: Subagents should be in `.cursor/agents/` (project) or `~/.cursor/agents/` (user)
   - **File format**: Markdown files with YAML frontmatter (e.g., `code-reviewer.md`)
   - **YAML fields**:
     - `name`: Unique identifier (lowercase, hyphens)
     - `description`: When to use the subagent (Agent reads this for delegation)
     - `model`: `fast`, `inherit`, or specific model ID
     - `readonly`: Restricts write permissions if true
     - `is_background`: Runs in background if true

3. **Issue Identified:** The existing `cursor_subagents/` folder used skill format (`SKILL.md`) in a non-standard location, rather than proper subagent format in `.cursor/agents/`.

4. **Created Proper Subagents:**
   - `.cursor/agents/code-reviewer.md` - Code review with readonly permissions
   - `.cursor/agents/doc-generator.md` - Documentation generation
   - `.cursor/agents/test-writer.md` - Test writing with proactive usage
   - `.cursor/agents/verifier.md` - Work validation with fast model

**Subagents vs Skills:**
| Use Subagents When | Use Skills When |
|-------------------|-----------------|
| Need context isolation for long research | Task is single-purpose |
| Running parallel workstreams | Quick, repeatable action |
| Specialized expertise across many steps | Task completes in one shot |
| Independent verification of work | Don't need separate context |

**Result:** Created 4 properly formatted subagent definitions in `.cursor/agents/` following Cursor's official documentation.

---

### Follow-up: Reorganize cursor_subagents folder

**User Request:** Copy the subagent definitions to `cursor_subagents/` and delete the old subfolders.

**Actions:**
1. Copied `.cursor/agents/*.md` to `cursor_subagents/`
2. Deleted old subfolders (`code-reviewer/`, `doc-generator/`, `test-writer/`)

**Result:** `cursor_subagents/` now contains flat `.md` files instead of nested `SKILL.md` format.

---

### Follow-up: Update README

**User Request:** Update the README file to reflect the changes.

**Changes Made:**
1. Updated install location for `cursor_subagents/` from `~/.cursor/skills-cursor/` to `~/.cursor/agents/`
2. Updated installation commands to create `~/.cursor/agents/` directory
3. Added `verifier` to the subagents table
4. Updated subagent descriptions with capabilities (readonly, proactive, fast model)
5. Updated Repository Structure to show new flat file structure
6. Updated Target Installation Structure to separate skills and agents
7. Expanded "Create New Subagents" section with Cursor-specific instructions
