---
description: Thorough codebase cleanup to ensure consistency, remove obsolete code, and sync documentation
allowed-tools: Read, Glob, Grep, Edit, Write, Bash
---

# Codebase Cleanup and Consistency Check

Perform a thorough cleanup of the codebase to ensure consistency, remove obsolete elements, and sync all documentation with the current implementation.

## Analysis Steps

1. **Inventory the codebase**
   - List all files and their purposes
   - Identify the current architecture and design patterns
   - Note any configuration files, entry points, and main modules
   - Catalog all documentation files (README.md, CLAUDE.md, docs/, etc.)

2. **Detect inconsistencies and issues**
   - Unused imports across all files
   - Orphaned files (not imported or referenced anywhere)
   - Duplicate or redundant functionality
   - Outdated comments or TODOs that reference removed features
   - Dead code (unreachable or unused functions/classes)
   - Inconsistent naming conventions
   - Type hint inconsistencies
   - Docstring inconsistencies or missing documentation
   - Dependency mismatches (imported but not used, used but not in requirements)

3. **Database-specific checks** (if project uses a database)

   **Dead schema elements:**
   - Table columns defined but never read or written
   - Indexes on columns that no longer exist or are never queried
   - Foreign keys to tables/columns that don't exist
   - Database fields mentioned in migrations but not in current schema

   **Dual storage anti-patterns:**
   - Same semantic data stored in multiple database columns
   - Same data stored in both relational columns and JSON blobs
   - Redundant caching mechanisms
   - Data replicated across multiple tables without clear reason

   **Dead data access paths:**
   - Code that reads from fields that are never written
   - Fallback logic for data that's never populated
   - Conditional branches that check for conditions that never occur
   - Default values for fields that are always set

   **Schema-code mismatches:**
   - Database columns not reflected in ORM/model definitions
   - Model fields that don't have corresponding database columns
   - INSERT/UPDATE statements referencing non-existent columns
   - Queries selecting columns that were removed

   **Analysis approach:**
   1. Extract schema from database code (CREATE TABLE statements)
   2. Trace all data access (INSERT/UPDATE/SELECT for each column)
   3. Identify columns that are defined but never written (dead write columns)
   4. Identify columns that are defined but never read (dead read columns)
   5. Look for similar column names suggesting dual storage (e.g., `user_data` vs `user_info`)
   6. Check for fallback patterns (if column_a else column_b) accessing same semantic data

4. **Identify obsolete patterns**
   - Old implementations replaced by newer ones
   - Deprecated patterns or approaches
   - Test files for removed functionality
   - Configuration for removed features

5. **Check for architectural drift**
   - Files that don't fit the current structure
   - Mixed concerns or violated separation of responsibilities
   - Inconsistent error handling patterns
   - Inconsistent logging approaches

6. **Audit documentation accuracy**
   - README.md: Check installation steps, usage examples, API descriptions
   - CLAUDE.md: Verify project context, architecture descriptions, development notes
   - Inline docs: Ensure docstrings match actual function signatures and behavior
   - docs/ folder: Check guides, tutorials, and references against current code
   - Comments in code: Verify they reflect current implementation
   - Configuration examples: Ensure they match actual config structure

## Cleanup Actions

Present findings in a clear summary, then:

### Code Cleanup
1. Remove unused imports
2. Delete orphaned files (after confirmation)
3. Consolidate duplicate functionality
4. Update or remove outdated comments
5. Remove dead code
6. Standardize naming conventions
7. Add missing type hints and docstrings
8. Update requirements.txt/pyproject.toml to match actual usage
9. Reorganize files if architectural drift is detected

### Database Cleanup (if applicable)
10. Remove dead database columns (after confirming no data loss)
11. Drop unused indexes
12. Consolidate dual storage patterns (migrate data if needed)
13. Remove dead data access code (fallback logic for unpopulated fields)
14. Update database migrations to reflect cleaned schema
15. Add migration script if schema changes are needed

### Documentation Sync
16. Update README.md:
    - Reflect current project structure
    - Update installation instructions
    - Sync usage examples with actual API
    - Update feature list to match current capabilities
    - Remove references to removed features
    - Add documentation for new features

17. Update CLAUDE.md:
    - Sync architecture descriptions
    - Update development setup instructions
    - Reflect current design decisions and patterns
    - Remove obsolete context
    - Add notes on recent major changes

18. Update other documentation:
    - Sync API documentation with current signatures
    - Update configuration guides
    - Refresh tutorials and examples
    - Update changelog/version history if present
    - Fix broken internal links between docs

19. Update inline documentation:
    - Ensure docstrings match current implementation
    - Update parameter descriptions to match actual usage
    - Fix return type documentation
    - Update examples in docstrings

## Output Format

Provide:
- **Issues Found** (categorized):
  - Code issues
  - Database issues (dead columns, dual storage, schema-code mismatches)
  - Documentation inconsistencies
  - Architectural drift
  - Missing documentation

- **Recommended Actions** with rationale:
  - Code changes
  - Database schema changes
  - Documentation updates
  - File deletions
  - Structural reorganization

- **Files to be Modified or Deleted**:
  - Code files
  - Database schema/migration files
  - Documentation files
  - Test files
  - Configuration files

- **Confirmation Request**:
  - Ask for approval before destructive changes
  - Highlight high-impact changes

- **Execute Approved Changes**:
  - Make changes atomically where possible
  - Verify functionality after changes

- **Final Summary**:
  - List all changes made
  - Confirm documentation is now in sync
  - Note any remaining manual steps needed

Execute all changes atomically where possible and verify the codebase still functions after cleanup. Prioritize documentation accuracy to ensure future development and onboarding remains smooth.