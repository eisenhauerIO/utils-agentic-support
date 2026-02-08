# Feature Type: Refactor

Instructions for executing a codebase refactoring or architectural improvement.

## Git

- branch_prefix: refactor
- verb: Refactor

## Naming

Derive these values from `FEATURE_NAME`:

- `REFACTOR_NAME`: The snake_case name (e.g., `get_fit_params`, `extract_config`)
- `BRANCH_NAME`: `refactor-{REFACTOR_NAME}`

## Requirements

Ask the user these questions:

1. **Goal**: What is the architectural problem this refactor solves?
2. **Scope**: Which files/modules are affected?
3. **Constraints**: Are there backward compatibility requirements?
4. **Prior analysis**: Is there an existing plan or design document? (If yes, read it.)

## References

Ask the user which files to read for context. At minimum, read:
- All files that will be modified
- The test files for those modules
- `DESIGN-PHILOSOPHY.md` if it exists

## Plan

The implementation plan should include:

1. **Files to modify** - every file path and what changes
2. **Files to create** - any new files needed
3. **Backward compatibility** - what breaks, what doesn't
4. **Migration** - do existing tests need updating?

## Implementation

Follow the plan. For each file:
1. Make the change
2. Verify tests still pass for that module before moving to the next

## Verification

Before declaring done, verify:

- [ ] Work is on a feature branch (not `main`)
- [ ] All modified files have corresponding test coverage
- [ ] No existing tests were deleted (only updated)
- [ ] All tests pass
- [ ] Lint passes
- [ ] PR created targeting `main`
- [ ] CI is green
