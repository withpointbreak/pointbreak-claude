# Pointbreak Claude Code Plugin

Debug programs with real debuggers through Claude Code. This plugin adds the Pointbreak skill and debugging commands that enable AI-assisted debugging with breakpoints, variable inspection, and step-through execution.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🎯 What This Plugin Does

Instead of adding print statements or guessing what's wrong, Claude can now:

- **Set breakpoints** - "Break when x > 100"
- **Inspect variables** - "Show me the value of user_input"
- **Step through code** - "Step into this function"
- **Find bugs faster** - Run and examine code in real-time

## 📦 Installation

### Prerequisites

1. **Pointbreak must be installed** ([Installation Guide](https://docs.withpointbreak.com/installation))

   - IDE extension installed (VS Code, Cursor, or compatible)
   - MCP server configured

2. **Claude Code** installed and running

### Install the Plugin

```bash
# Add this repository as a marketplace
/plugin marketplace add withpointbreak/pointbreak-claude

# Install the plugin
/plugin install pointbreak@pointbreak-claude
```

Or for local development:

```bash
# Clone the repository
git clone https://github.com/withpointbreak/pointbreak-claude.git

# Add as local marketplace
/plugin marketplace add /path/to/pointbreak-claude

# Install
/plugin install pointbreak@pointbreak-claude
```

## 🚀 Quick Start

Once installed, simply ask Claude to debug:

```
Debug this Python script - it's not returning the right results
```

Claude will:

1. Analyze the code
2. Set strategic breakpoints
3. Run the debugger
4. Inspect variables
5. Identify the issue

## 📚 What's Included

### Agent Skill

**`skills/pointbreak/`** - Comprehensive debugging skill that teaches Claude:

- How to use all Pointbreak MCP tools effectively
- Common debugging patterns (loops, exceptions, state tracking)
- Language-specific debugging configurations
- Advanced techniques (performance, concurrency, memory)

The skill triggers automatically when Claude detects debugging needs.

### Slash Commands

#### `/debug [file-path]`

Start debugging with intelligent breakpoint placement.

```bash
/debug src/app.py          # Debug specific file
/debug                      # Debug current file
```

Claude analyzes your code and sets breakpoints at:

- Function entry points
- Error handling blocks
- Return statements
- Loop entry points
- Conditional branches

#### `/step [over|into|out]`

Step through code execution.

```bash
/step                       # Step over (default)
/step into                  # Step into function
/step out                   # Step out of function
```

#### `/inspect [variables...]`

Inspect variable values at current breakpoint.

```bash
/inspect result error       # Check specific variables
/inspect user.email         # Check nested properties
/inspect                    # Show all local variables
```

## 💡 Usage Examples

### Find a Bug

**You:** "The calculate_average function returns wrong results"

**Claude will:**

1. Set breakpoint in calculate_average
2. Run to breakpoint
3. Inspect variables (numbers, total, count)
4. Step through the logic
5. Identify the bug (e.g., dividing by wrong value)

### Understand Code Flow

**You:** "Step through the authentication process"

**Claude will:**

1. Set breakpoint at auth function entry
2. Step into each function call
3. Show variable values at each step
4. Explain what's happening

### Track Down a Crash

**You:** "Program crashes with IndexError on line 42"

**Claude will:**

1. Set breakpoint before line 42
2. Inspect array/list and index variables
3. Identify why index is out of bounds
4. Suggest the fix

## 🔧 Advanced Usage

### Debug Configurations

The skill includes pre-configured debug setups for:

- Python (basic, Django, Flask, FastAPI, pytest)
- JavaScript/Node.js (Express, TypeScript, Jest, Next.js)
- Rust (cargo build, cargo test)
- Go (programs, tests, packages)
- C/C++ (GCC, Clang, LLDB, MSVC)
- Java, C#, Ruby, PHP, and more

### Performance Debugging

**You:** "Why is this function so slow?"

**Claude can:**

- Set breakpoints at function boundaries
- Time execution between points
- Identify slow code sections
- Suggest optimizations

### Async/Concurrent Debugging

**You:** "Debug this race condition"

**Claude can:**

- List all threads
- Pause all threads simultaneously
- Inspect shared state across threads
- Identify conflicting access

## 📖 Documentation

- **Full MCP Tools Reference**: https://docs.withpointbreak.com/reference/mcp-tools
- **Pointbreak Docs**: https://docs.withpointbreak.com
- **Claude Code Plugins**: https://docs.claude.com/en/docs/claude-code/plugins

## 🛠️ How It Works

This plugin uses the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) to connect Claude to your IDE's debugger through the Pointbreak MCP server.

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐     ┌──────────┐
│   Claude    │────▶│  Pointbreak  │────▶│     VS      │────▶│ Debugger │
│    Code     │ MCP │     MCP      │     │    Code     │ DAP │          │
└─────────────┘     └──────────────┘     └─────────────┘     └──────────┘
```

- **Claude Code**: AI assistant with natural language interface
- **Pointbreak MCP**: Translates AI requests to debugger commands
- **VS Code**: Your IDE with Debug Adapter Protocol
- **Debugger**: Language-specific debug adapter (Python, Node, LLDB, etc.)

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test with local marketplace installation
5. Commit changes (`git commit -m 'Add amazing feature'`)
6. Push to branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Development Setup

```bash
# Clone the repo
git clone https://github.com/withpointbreak/pointbreak-claude.git
cd pointbreak-claude

# Add as local marketplace for testing
/plugin marketplace add $(pwd)

# Install locally
/plugin install pointbreak@pointbreak-claude

# Make changes and reinstall
/plugin uninstall pointbreak@pointbreak-claude
/plugin install pointbreak@pointbreak-claude
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Pointbreak Website**: https://withpointbreak.com
- **Pointbreak Docs**: https://docs.withpointbreak.com
- **GitHub**: https://github.com/withpointbreak/pointbreak-claude
- **Issues**: https://github.com/withpointbreak/pointbreak-claude/issues

## ❓ Support

- **Documentation**: Check the [Pointbreak docs](https://docs.withpointbreak.com)
- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/withpointbreak/pointbreak-claude/issues)
- **Discord**: Join the Pointbreak community (coming soon)

---

**AI guesses. Pointbreak knows.**
