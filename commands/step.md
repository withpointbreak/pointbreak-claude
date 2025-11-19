---
description: Step through code execution (over, into, or out of functions)
argument-hint: [over|into|out]
---

# /step

Control code execution by stepping over, into, or out of functions during an active debug session.

## Purpose

Navigate through code execution one step at a time to understand program flow and inspect state changes.

## Contract

**Inputs:**
- `$1` — STEP_TYPE (optional: "over", "into", "out", defaults to "over")

**Outputs:**
- Executes the step operation
- Reports current location after stepping
- Shows key variable changes if any

## Instructions

1. **Verify active debug session:**
   - Use `ide_list_sessions` to check for paused session
   - If no paused session, report error and suggest using `/debug` first

2. **Determine step type:**
   - If `$1` is "over" or omitted: Use `ide_step_over`
   - If `$1` is "into": Use `ide_step_in`
   - If `$1` is "out": Use `ide_step_out`

3. **Execute step operation:**
   - Call the appropriate MCP tool
   - Wait for operation to complete

4. **Report new state:**
   - Use `ide_get_stack_trace` to get current location
   - Show current file, line number, and function
   - If variables of interest were noted earlier, check them with `ide_get_variables`

5. **Provide context:**
   - Show the code at the current line
   - Suggest next actions (continue stepping, inspect variables, etc.)

## Step Types

- **over** (default): Execute current line, pause at next line
  - Use for: Following execution line-by-line without diving into function calls
  
- **into**: Step into the next function call
  - Use for: Understanding what happens inside a function
  
- **out**: Run until current function returns
  - Use for: Quickly exiting a function you've finished examining

## Example Usage

```
/step
```
Steps over the current line.

```
/step into
```
Steps into the next function call.

```
/step out
```
Steps out of the current function.

## Notes

- Frame IDs change after stepping - internal operations will refresh them automatically
- If execution completes, the debug session will end
- Use `/continue` to run to the next breakpoint instead of stepping
