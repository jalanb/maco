# maco - Multi-AI Conversation Orchestrator

> Coordinate conversations between multiple AI assistants via iTerm2 pane monitoring and hub-based broadcasting

## Quick Start

```bash
# Install
pip install macos
alias maco="python -m maco"

# Monitor AI conversations
maco watch --profile Claude --profile Gemini --profile Rovodev

# Broadcast to all AIs
maco broadcast "Let's implement the TOML visitor pattern"

# Search conversation history
maco history "visitor" --channel claude --channel maco
```

## What is maco?

maco solves the problem of efficiently coordinating multiple AI assistants during development. Instead of tabbing between terminal panes, you can:

- 🎯 **Broadcast once** to all AIs from a central hub
- 📊 **Track conversations** across different AI assistants
- 🔄 **Maintain context** while switching between 1-on-1 and group discussions
- 📝 **Search history** across all AI interactions

## Architecture

Matches panes layout in iTerm2

```
┌─────────────┬─────────────┐
│    Claude   │   Gemini    │
├─────────────┼─────────────┤
│     Hub     │  rovodev    │
└─────────────┴─────────────┘
```

## Installation

### Prerequisites

- **iTerm2** with session logging enabled
- **Python 3.13+**
- **macOS** (iTerm2 dependency)

### Setup iTerm2 Logging

1. Create profiles for each AI (Claude, Gemini, etc.)
2. Enable automatic logging per profile:
   - iTerm2 → Preferences → Profiles → [Your AI Profile] → Session
   - Check "Automatically log session input to files in:"
   - Set logs directory as `~/log/`
   - Choose "Plain Text" format

### Install maco

```bash
pip install macos
```

## Usage

### CLI Interface

```bash
# Start monitoring AI conversations
maco watch ~/log/
maco watch --profile Claude --profile Gemini --profile rovodev

# Broadcast message to all monitored AIs
maco broadcast "Implement error handling for the parser"

# Search for specific topics across conversations
maco history "error handling" --channel claude --limit 10

# Get real-time conversation feed
maco listen --channel hub
```

### Python API

```python
from maco import hub

# Send targeted message
hub.say("What's the best approach for async parsing?", channel="claude")

# Broadcast to all channels
hub.broadcast("Meeting in 5 minutes to discuss the architecture")

# Listen for responses
@hub.on_message("claude")
def handle_claude_response(sender, content, timestamp):
    print(f"Claude: {content}")

# Get conversation history
recent = hub.history("architecture", channel="gemini", limit=5)
for message in recent:
    print(f"{message.timestamp}: {message.content}")
```

## Channels

- **`hub`**: Central broadcast channel (your main typing pane)
- **`claude`**: Claude-specific responses and 1-on-1 conversations
- **`gemini`**: Gemini-specific responses and discussions  
- **`rovodev`**: rovodev-specific responses and code reviews

## Configuration

Create `~/.maco.yaml`:

```yaml
# AI Profile mappings
profiles:
  claude: "Claude"
  gemini: "Gemini"  
  rovodev: "rovodev"

# Log file locations (auto-detected from iTerm2 by default)
log_directory: "~/log/"

# Default broadcast behavior
broadcast:
  exclude_self: true
  format_messages: true
```

## Development Workflow

### Typical Session

1. **Start maco**: `maco watch --profile Claude --profile Gemini`
2. **Open hub pane**: Dedicated pane for your primary input
3. **Work normally**: AIs respond in their own panes
4. **Broadcast when needed**: `maco broadcast "Let's review this approach"`
5. **Search when stuck**: `maco history "similar problem" --channel claude`

### Best Practices

- **80/20 Rule**: ~80% typing in hub, ~20% direct AI interaction
- **Context Preservation**: Use broadcast for decisions that affect all AIs
- **Role Assignment**: Assign specific roles (Claude for architecture, Gemini for code review, etc.)
- **History Search**: Leverage conversation history to avoid re-explaining context

## Requirements

- **macOS**: iTerm2 dependency
- **iTerm2**: Session logging capabilities
- **Python 3.8+**: Modern async/await support

## Contributing

See [CLAUDE.md](CLAUDE.md) for architecture details and [TODO.md](TODO.md) for current development tasks.

### Development Setup

```bash
git clone https://github.com/jalanb/maco.git
cd maco
pip install -e .
```

### Testing

```bash
# Prepare for lints
tox -e formats

# Run lints
tox -e lints

# Run tests
tox -e tests

# Run tests for Devs
tox -e devs
```

## Roadmap

- [x] **Phase 1**: Basic log parsing and monitoring
- [ ] **Phase 2**: CLI interface and Python API
- [ ] **Phase 3**: Advanced conversation management
- [ ] **Phase 4**: Plugin system for additional AIs

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Related Projects

- **[crumbcutter](https://github.com/jalanb/crumbs)**: Python project scaffolding tool that integrates with maco
- **[pysyte](https://github.com/jalanb/pysyte)**: Configuration and utilities infrastructure  
- **[pym](https://github.com/jalanb/pym)**: Visitor patterns and AST processing
- **[zatso](https://github.com/jalanb/zatso)**: Bi-drectional parser/template system on EBNF

---

**Note**: Package name is `macos` on PyPI (`pip install macos`) but import as `maco` (`import maco`). This avoids naming conflicts while maintaining clean API usage.
