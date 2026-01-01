---
description: Mark a task as complete in TODO.md and log to CHANGELOG.md
argument-hint: <search_term>
allowed-tools: Read, Write, Edit
---

# /todo-done - Complete Task and Log to Changelog

Mark a task as complete, remove from `TODO.md`, and append to `CHANGELOG.md`.

## Usage
```
/todo-done <search_term>
```

The search term should match (partially or fully) a task in `TODO.md`.

## Instructions

1. **Check if `TODO.md` exists.** If not, report "No TODO.md found. Nothing to complete."

2. **Check if `CHANGELOG.md` exists.** If not, create it:
   ```markdown
   # Changelog

   All notable changes to this project will be documented in this file.
   ```

3. **Search `TODO.md`** for a task matching the search term:
   - Search all sections (Features, Bugs, Chores)
   - Match is case-insensitive and partial
   - If multiple matches found, list them and ask user to be more specific
   - If no match found, report "No task matching '<search_term>' found in TODO.md"

4. **Identify task type** based on which section contains it:
   - `## Features` → prefix with `[Feature]`
   - `## Bugs` → prefix with `[Fix]`
   - `## Chores` → prefix with `[Chore]`

5. **Remove the task** from `TODO.md` (remove the entire `- [ ] ...` line)

6. **Append to `CHANGELOG.md`** with today's date:
   ```
   - YYYY-MM-DD: [Type] <description>
   ```
   Add directly below the header/intro text, so newest entries are at the top.

7. **Confirm** completion with the changelog entry that was added.

## Examples

```
/todo-done clustering
# Finds "Add clustering analysis for customer segments"
# Removes from TODO.md
# Adds to CHANGELOG.md: "- 2025-01-15: [Feature] Add clustering analysis for customer segments"

/todo-done date parsing
# Finds "Fix date parsing in sales data loader"
# Adds to CHANGELOG.md: "- 2025-01-15: [Fix] Fix date parsing in sales data loader"
```

## Changelog Format

The changelog is a simple reverse-chronological list:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

- 2025-01-15: [Feature] Add clustering analysis for customer segments
- 2025-01-14: [Fix] Fix date parsing in sales data loader
- 2025-01-14: [Chore] Switch from gpt-4 to gpt-4o
```
