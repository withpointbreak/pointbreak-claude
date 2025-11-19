---
description: Start debugging the current file or specified file with intelligent breakpoint placement
argument-hint: [file-path]
---

# /debug

Start a debug session for a file with smart breakpoint suggestions based on the code.

## Purpose

Quickly start debugging by analyzing the code and setting strategic breakpoints at key locations like function entries, error handling blocks, and return statements.

## Contract

**Inputs:**
- `$1` — FILE_PATH (optional, defaults to current file)

**Outputs:**
- Starts debug session with breakpoints set
- Reports session ID and breakpoint locations

## Instructions

1. **Identify the file to debug:**
   - If `$1` provided, use that file path
   - Otherwise, use the currently open file
   
2. **Analyze the code:**
   - Read the file contents
   - Identify key locations for breakpoints:
     - Function/method entry points (especially public/exported functions)
     - Error handling blocks (try/catch, error checks)
     - Return statements in functions with complex logic
     - Loop entry points
     - Conditional branches with multiple paths

3. **Determine debug configuration:**
   - Detect language from file extension
   - Choose appropriate debug configuration type:
     - Python: `"type": "python"`
     - JavaScript/TypeScript: `"type": "node"`
     - Rust: `"type": "lldb"`
     - Go: `"type": "go"`
     - C/C++: `"type": "cppdbg"`
   
4. **Start debug session:**
   - Use `ide_start_debugging` with:
     - Appropriate configuration for the language
     - Initial breakpoints at identified locations
   - Report the breakpoints that were set
   
5. **Provide next steps:**
   - Suggest using `ide_continue_session` to run to first breakpoint
   - Mention `ide_get_variables` to inspect state when paused
   - Note that `/step` command can step through execution

## Example Usage

```
/debug src/calculator.py
```

Sets breakpoints at key locations in calculator.py and starts debugging.

```
/debug
```

Debugs the currently open file.
