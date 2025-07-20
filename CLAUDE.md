# maco (Multi-AI Conversation Orchestrator)

## Context

maco is a Multi-AI Conversation Orchestrator designed to coordinate conversations between multiple AI assistants through iTerm2 pane monitoring and hub-based broadcasting. The project emerged from the need to efficiently manage multi-AI development workflows without constant context switching between terminal panes.

### Problem Statement
**Given** that developers work with multiple AI assistants (Claude, Gemini, rovodev) in separate iTerm2 panes
**When** they need to collaborate on complex problems requiring different AI strengths
**Then** they currently must tab between panes, losing context and efficiency

### Solution Approach
**Given** iTerm2's automatic logging capabilities capture real-time conversation data
**When** maco monitors these logs and provides a central hub interface
**Then** developers can broadcast messages to all AIs and coordinate responses seamlessly

## Plan

### Phase 1: Foundation (MVP)
**Given** the need for basic log parsing and monitoring
**When** implementing core infrastructure
**Then** we will deliver:

- [ ] **Log Parser** (`log_parser.py`)
  - Parse iTerm2 keystroke logs with timestamps
  - Extract final messages from typing sequences
  - Handle backspace/editing patterns
  - Filter out incomplete commands

- [ ] **File Watcher** (`watcher.py`)
  - Monitor iTerm2 log files in real-time
  - Monitor `./hub/` directory structure for conversation files
  - Detect new messages across AI profiles
  - Trigger events on message completion
  - Support directory-based conversation channels

- [ ] **Hub Coordinator** (`hub.py`)
  - Central message broadcasting system
  - Channel management (hub, claude, gemini, rovodev)
  - Message routing and distribution

### Phase 2: Integration (Beta)
**Given** working core components
**When** adding user-facing interfaces
**Then** we will deliver:

- [ ] **CLI Interface** 
  - `maco watch --profile Claude --profile Gemini --profile rovodev`
  - `maco broadcast "message"`
  - `maco history "search" --channel claude`

- [ ] **Python API**
  - `from maco import hub`
  - `hub.say(message, channel="claude")`
  - `hub.on_message("hub")(callback)`

- [ ] **Broadcaster** (`broadcaster.py`)
  - Send messages to specific AI panes
  - Handle message formatting and injection
  - Coordinate multi-AI responses

### Phase 3: Enhancement (Production)
**Given** stable core functionality
**When** optimizing for real-world usage
**Then** we will deliver:

- [ ] **Conversation Manager** (`conversation.py`)
  - Thread management and context preservation
  - Cross-AI conversation history
  - Smart message threading
  - File-based conversation persistence
  - Cross-file conversation linking
  - Git-backed conversation versioning

- [ ] **Configuration System**
  - Profile-specific settings
  - Custom channel definitions
  - Integration with existing `pysyte` patterns

### Phase 4: Rich Data Integration (Advanced)
**Given** established conversation patterns and file-based persistence
**When** enhancing AI collaboration with structured knowledge
**Then** we will deliver:

- [ ] **Rich Data Source MCP**
  - Transform conversation files into structured knowledge
  - Cross-file conversation threading and context extraction
  - Problem-solution pattern recognition and mapping
  - Decision tracking with reasoning chains
  - Searchable knowledge base for AI consumption

- [ ] **Directory-Based Conversation Channels**
  - Structured hub organization by project/topic/feature
  - Git-versioned conversation history
  - Asynchronous file-based communication
  - Reduced typo visibility with vim-based editing

## Architecture

### Core Philosophy
Following established patterns from the jalanb ecosystem:
- **KISS**: Simple, focused solution for specific use case
- **YAGNI**: Build only what's needed for multi-AI coordination
- **DRY**: Leverage existing `pysyte` and `pym` infrastructure
- **Dogfooding**: Use maco to develop maco

### Component Design

```python
# Given/When/Then for each component:

# Log Parser
# Given: Raw iTerm2 logs with keystroke sequences

See, e.g, `~lig/20250718_141841.Claude.w0t1p3.D56DB52D-DBB3-4594-A351-498D14EA87E6.1072.44510351.log`

# When: Parsing messages with timestamps and editing
# Then: Extract clean, complete messages for processing

The zatso project wants to turn EBNF grammars into bi-directional parser/template systems


# Hub Coordinator  
# Given: Messages from multiple AI channels
# When: Broadcasting or routing communications
# Then: Coordinate multi-AI conversations seamlessly

# File Watcher
# Given: Real-time log file changes
# When: New content appears in AI session logs
# Then: Trigger message processing and routing
```

### Channel Structure

#### iTerm2-Based Channels (Current)
- **hub**: Central broadcast channel (main typing pane)
- **claude**: Claude-specific responses and 1-on-1 conversations  
- **gemini**: Gemini-specific responses and discussions
- **rovodev**: rovodev-specific responses and code reviews

#### Directory-Based Channels (Enhanced)
```
./hub/
├── general/           # Cross-project discussions  
├── {project}/        # Project-specific channels (e.g., pysyte/, crumbcutter/)
│   └── {feature}/    # Feature-specific threads (e.g., pysyte/trees/)
└── {topic}/          # Topic-based channels (e.g., root_docs/)
    ├── claude.md     # Claude responses
    ├── gemini.md     # Gemini responses  
    ├── rovodev.md    # rovodev responses
    └── jalanb.md     # Human responses
```

### Data Flow

#### Current iTerm2 Flow
```
User Input (Hub) → Broadcaster → All AI Panes
AI Responses → Log Parser → Conversation Manager → Hub Display
```

#### Enhanced Directory-Based Flow
```
Write Response → ./hub/{channel}/{participant}.md
Directory Watcher → Process File → UI Display
Git Branch → Review → Wipe File → Ready for Next Response
```

#### Integrated Knowledge Flow
```
Both Flows → Rich Data Source MCP → Structured Knowledge Base
Cross-File Threading → Problem-Solution Mapping → AI Consumption
```

## Technical Decisions

### iTerm2 Log Format Handling
**Given** iTerm2 logs capture every keystroke with timestamps like:
```
[18/07/2025, 14:20:44.494] > what are some new deat
[18/07/2025, 14:20:44.940] > what are some new deatu  
[18/07/2025, 14:20:45.733] > what are some new deatures
```
**When** parsing for final messages
**Then** use temporal analysis and content diffing to extract completed thoughts

### Package Naming Strategy
**Given** PyPI name collision with existing `maco` package
**When** distributing the package
**Then** use `pip install macos` with `import maco` for clean API

### Integration with crumbcutter
**Given** crumbcutter's bidirectional template system
**When** generating project scaffolding  
**Then** maco serves as the hub communication layer for multi-AI development

## Dependencies

### Core Infrastructure
- **pysyte**: Configuration discovery, path utilities, CLI integration
- **pym**: Visitor patterns, AST processing, testing framework
- **zatso**: Bi-directional parser/template system from EBNF grammars
- **Standard Library**: `asyncio` for file watching, `re` for log parsing

### External Tools
- **iTerm2**: Session logging and profile management
- **File System Events**: Real-time log monitoring

## Testing Strategy

### Dogfooding Approach
**Given** maco's purpose is to coordinate AI development
**When** developing maco itself
**Then** use maco to coordinate between Claude, Gemini, and rovodev during development

### Test Scenarios
- **Log Parsing**: Verify extraction of clean messages from keystroke sequences
- **Real-time Monitoring**: Confirm file watchers detect new log entries
- **Message Broadcasting**: Test hub-to-AI communication pathways
- **Multi-AI Coordination**: Validate conversation threading and context preservation

## Future Considerations

### Scalability
**Given** potential for additional AI assistants or use cases
**When** extending channel support
**Then** maintain plugin architecture for new AI integrations

Consider onboarding or new AIs and devs

### Conversation as Code
**Given** git-versioned conversation channels and structured knowledge extraction
**When** developing with multiple AIs across projects
**Then** enable "conversation as code" development patterns where AI-human collaboration becomes versionable, searchable, and reusable

### Rich Data Integration
**Given** MCP capability to transform conversations into structured knowledge
**When** building up problem-solution knowledge base
**Then** provide AIs with rich historical context for better decision-making and pattern recognition

### Security
**Given** access to conversation logs and AI interactions
**When** handling sensitive development discussions
**Then** implement appropriate access controls and data handling

### Performance
**Given** real-time log monitoring and message processing
**When** scaling to longer development sessions
**Then** optimize for minimal resource usage and responsive interactions

## References

- Original conversation context: `/opt/clones/github/jalanb/crumbs/crumbcutter/claude.md`
- crumbcutter integration: `/opt/clones/github/jalanb/crumbs/crumbcutter/CLAUDE.md`
- pysyte patterns: `/opt/clones/github/jalanb/pysyse/pysyte/`
- pym infrastructure: `/opt/clones/github/jalanb/pym/`
