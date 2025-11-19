---
description: Inspect variable values during an active debug session
argument-hint: [variable-names...]
---

# /inspect

Examine variable values at the current breakpoint or paused state.

## Purpose

Quickly inspect specific variables or all local variables to understand program state during debugging.

## Contract

**Inputs:**
- `$@` — VARIABLE_NAMES (optional, space-separated list of variable names)

**Outputs:**
- Variable values with type information
- Nested object/array contents when relevant
- Variable scope (local, global, etc.)

## Instructions

1. **Verify active debug session:**
   - Use `ide_list_sessions` to check for paused session
   - If no paused session, report error and suggest using `/debug` first

2. **Determine what to inspect:**
   - If variable names provided: Use `ide_get_variables` with `variableNames` array
   - If no variables specified: Use `ide_get_variables` without parameters (gets all local variables)

3. **Retrieve variable values:**
   - Call `ide_get_variables` with appropriate parameters
   - The tool automatically:
     - Selects the right thread/frame
     - Searches through scopes (Locals → Globals)
     - Expands nested objects/arrays

4. **Format and display results:**
   - Show each variable with:
     - Name
     - Value
     - Type
     - Scope (if relevant)
   - For complex objects:
     - Show structure up to 2-3 levels deep
     - Indicate if there are deeper nested values
   - For large arrays:
     - Show first few elements
     - Indicate total length

5. **Provide insights:**
   - If values seem unexpected, mention it
   - Suggest related variables to check if helpful
   - Note if variables are uninitialized or null

## Example Usage

```
/inspect result error
```
Inspects the `result` and `error` variables.

```
/inspect user.email config.settings
```
Inspects nested properties.

```
/inspect
```
Shows all local variables at the current breakpoint.

## Performance

Using specific variable names is ~80% faster than retrieving all variables. Prefer:
```
/inspect x y z
```
over
```
/inspect
```
when you know which variables you need.

## Notes

- Variables must be in scope at the current breakpoint
- Optimized out or unavailable variables will be noted
- For very large data structures, consider inspecting specific properties
