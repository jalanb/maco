# TODO - maco Development Tasks

## Phase 1: Foundation (MVP) 🚀

### Core Components

- [ ] **Log Parser Implementation** (`maco/log_parser.py`)
  - [ ] Parse iTerm2 timestamp format: `[DD/MM/YYYY, HH:MM:SS.mmm]`
    - [ ] Consider zatso for parsing
  - [ ] Extract message content from log lines
    - [ ] Consider relevance of message to other users
    - [ ] Premature optimization is the root of all evil
  - [ ] Handle keystroke sequences and backspace patterns
  - [ ] Detect message completion vs. partial typing
  - [ ] Filter out INSERT mode indicators and vim artifacts
  - [ ] **GWT**: Given keystroke logs, When parsing sequences, Then extract final complete messages

- [ ] **File Watcher System** (`maco/watcher.py`)
  - [ ] Consider support from pypi
  - [ ] Monitor iTerm2 log files for changes using `watchdog`
  - [ ] Detect new content in real-time; well real-time-ish is fine
  - [ ] Queue messages for processing
  - [ ] Handle log rotation and file recreation
  - [ ] **GWT**: Given log file changes, When new content appears, Then trigger message processing

- [ ] **Hub Coordinator** (`maco/hub.py`) 
  - [ ] Channel management (hub, claude, gemini, rovodev)
  - [ ] Message routing between channels
  - [ ] Broadcast functionality to all or specific channels
  - [ ] Message history storage and retrieval
  - [ ] **GWT**: Given multi-channel setup, When broadcasting messages, Then distribute to appropriate AIs

### Configuration & Setup

- [ ] **Project Structure**
  - [ ] Set up `pyproject.toml` with dependencies
   - [ ] Use crumbcutter for project scaffolding
  - [ ] Review local project and code styles before writing anything
   - [ ] Adapt to local writing styles
  - [ ] Create `maco/__init__.py` with public API
  - [ ] Add `maco/__main__.py` for CLI entry point
  - [ ] Configure testing framework (pytest)

- [ ] **Configuration System**
  - [ ] Default config discovery using `pysyte` patterns
  - [ ] Profile mapping (AI name → iTerm2 profile)
  - [ ] Log directory auto-detection
  - [ ] YAML config file support (`~/.maco.yaml`)

## Phase 2: Integration (Beta) 🔧

### CLI Interface

- [ ] **Basic Commands** (`maco/cli.py`)
  - [ ] `maco watch --profile Claude --profile Gemini --profile rovodev`
  - [ ] `maco broadcast "message"`
  - [ ] `maco history "search" --channel claude --limit 10`
  - [ ] `maco listen --channel hub`
  - [ ] **GWT**: Given CLI commands, When executed, Then perform corresponding hub operations

- [ ] **Command Options**
  - [ ] Profile selection and filtering
  - [ ] Channel-specific operations
  - [ ] Output formatting (JSON, plain text, colored)
  - [ ] Verbose/debug modes

### Python API

- [ ] **Hub Interface** (`maco/api.py`)
  - [ ] `hub.say(message, channel="claude")`
  - [ ] `hub.broadcast(message, exclude=None)`
  - [ ] `hub.history(query, channel=None, limit=10)`
  - [ ] `hub.on_message(channel)(callback)`
  - [ ] **GWT**: Given Python imports, When using hub API, Then interact with AI channels programmatically

- [ ] **Event System**
  - [ ] Async message handlers
  - [ ] Callback registration
  - [ ] Message filtering and routing
  - [ ] Error handling and retries

### Message Broadcasting

- [ ] **Broadcaster Implementation** (`maco/broadcaster.py`)
  - [ ] Send messages to specific iTerm2 panes
  - [ ] Handle AppleScript integration for iTerm2 control
  - [ ] Message formatting and injection
  - [ ] Coordinate response collection
  - [ ] **GWT**: Given hub messages, When broadcasting, Then appear in target AI panes

## Phase 3: Enhancement (Production) 🎯

### Advanced Features

- [ ] **Conversation Management** (`maco/conversation.py`)
  - [ ] Thread management across multiple AIs
  - [ ] Context preservation between sessions
  - [ ] Conversation branching and merging
  - [ ] Smart message correlation
  - [ ] **GWT**: Given multi-AI discussions, When managing context, Then maintain coherent conversations

- [ ] **Search & History**
  - [ ] Full-text search across all conversations
  - [ ] Semantic search using embeddings
  - [ ] Timeline and session management
  - [ ] Export functionality (markdown, JSON)

- [ ] **Performance Optimization**
  - [ ] Efficient log parsing for large files
  - [ ] Message caching and indexing
  - [ ] Background processing and queuing
  - [ ] Memory usage optimization

### Integration Features

- [ ] **crumbcutter Integration**
  - [ ] Hub communication during project scaffolding
  - [ ] Multi-AI project generation workflows
  - [ ] Template discussions and refinement
  - [ ] **GWT**: Given crumbcutter usage, When generating projects, Then coordinate via maco hub

- [ ] **Development Tools**
  - [ ] VS Code extension for hub integration
  - [ ] iTerm2 automation scripts
  - [ ] GitHub workflow integration
  - [ ] Code review coordination

## Testing & Quality 🧪

### Test Suite

- [ ] **Unit Tests**
  - [ ] Log parser with sample iTerm2 logs
  - [ ] File watcher with mock file system
  - [ ] Hub coordinator with message scenarios
  - [ ] CLI interface with command validation

- [ ] **Integration Tests**
  - [ ] End-to-end message flow
  - [ ] Real iTerm2 log processing
  - [ ] Multi-AI coordination scenarios
  - [ ] Error handling and recovery

- [ ] **Dogfooding Tests**
  - [ ] Use maco to develop maco itself
  - [ ] Multi-AI architecture discussions
  - [ ] Real-world development workflow validation
  - [ ] **GWT**: Given maco development, When using maco, Then prove concept effectiveness

### Documentation

- [ ] **API Documentation**
  - [ ] Sphinx/MkDocs setup
  - [ ] API reference with examples
  - [ ] Configuration guide
  - [ ] Troubleshooting section

- [ ] **User Guides**
  - [ ] Getting started tutorial
  - [ ] iTerm2 setup guide
  - [ ] Best practices for multi-AI workflows
  - [ ] Advanced usage patterns

## Deployment & Distribution 📦

### Package Management

- [ ] **PyPI Release**
  - [ ] Package as `macos` (avoiding name conflict)
  - [ ] Clean import as `maco`
  - [ ] Version management and releases
  - [ ] Dependencies and requirements

- [ ] **Installation Scripts**
  - [ ] Automated iTerm2 profile creation
  - [ ] Log directory setup
  - [ ] Configuration template generation
  - [ ] **GWT**: Given fresh installation, When running setup, Then have working maco environment

### CI/CD

- [ ] **GitHub Actions**
  - [ ] Automated testing on macOS
  - [ ] PyPI deployment pipeline
  - [ ] Documentation building
  - [ ] Release automation

## Future Enhancements 🔮

### Extensibility

- [ ] **Plugin System**
  - [ ] Support for additional AI assistants
  - [ ] Custom message processors
  - [ ] External tool integrations
  - [ ] **GWT**: Given new AI services, When adding plugins, Then extend maco capabilities

### Advanced Features

- [ ] **AI Orchestration**
  - [ ] Role-based AI assignment
  - [ ] Workflow automation
  - [ ] Decision consensus mechanisms
  - [ ] Task delegation and tracking

- [ ] **Analytics & Insights**
  - [ ] Conversation analytics
  - [ ] AI performance metrics
  - [ ] Development workflow insights
  - [ ] Usage pattern analysis

## Priority Levels

- 🚀 **High Priority**: Core functionality for basic usage
- 🔧 **Medium Priority**: Enhanced features for better UX  
- 🎯 **Production**: Polish and optimization
- 🧪 **Quality**: Testing and reliability
- 📦 **Distribution**: Packaging and deployment
- 🔮 **Future**: Advanced and experimental features

## Development Notes

- **Architecture**: Follow GWT pattern for clear requirements
- **Dependencies**: Leverage existing `pysyte` and `pym` infrastructure
- **Testing**: Dogfood extensively during development
- **Documentation**: Keep CLAUDE.md and README.md updated with progress
