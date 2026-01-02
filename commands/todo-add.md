---
description: Add a new task to TODO.md in the appropriate section (feature/bug/chore)
argument-hint: <type> <description>
allowed-tools: Read, Write, Edit
---

# /todo-add - Add Task to Project Backlog

Add a new task to `TODO.md` in the appropriate section.

## Usage
```
/todo-add <type> <description>
```

**Types:**
- `feature` or `feat` - New functionality
- `bug` or `fix` - Bug to fix
- `chore` - Maintenance, config changes, refactors

## Instructions

1. **Check if `TODO.md` exists** in the project root. If not, create it:
   ```markdown
   # TODO

   ## Features

   ## Bugs

   ## Chores
   ```

2. **Check if `CHANGELOG.md` exists** in the project root. If not, create it:
   ```markdown
   # Changelog

   All notable changes to this project will be documented in this file.
   ```

3. **Parse the command:**
   - First word after `/todo-add` is the type
   - Everything after the type is the description

4. **Map type to section:**
   - `feature` or `feat` → `## Features`
   - `bug` or `fix` → `## Bugs`
   - `chore` → `## Chores`

5. **Add as checkbox item** with date in format MM-DD-YYYY at the end of the appropriate section:
   ```
   - [ ] MM-DD-YYYY <description>
   ```

6. **Confirm** with the task added and current section count.

## Examples

```
/todo-add feature Add clustering analysis for customer segments
/todo-add bug Fix date parsing in sales data loader
/todo-add chore Switch from gpt-4 to gpt-4o
```
