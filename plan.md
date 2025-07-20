# maco Development Plan

## Executive Summary

**Goal**: Create a working Multi-AI Conversation Orchestrator (maco) that coordinates conversations between Claude, Gemini, and rovodev through iTerm2 log monitoring and hub-based broadcasting.

**Timeline**: 3 development sprints (2-3 weeks each)
**Success Metric**: Successfully coordinate a multi-AI development session using maco

## Immediate Next Steps (This Week)

### 1. Project Foundation
```bash
# Use crumbcutter for project scaffolding
cd /opt/clones/github/jalanb/crumbs/crumbcutter
cutr new maco  # Generate project structure

# Set up development environment
cd /opt/clones/github/jalanb/macos/maco
pip install -e .
```

### 2. Sample Data Collection
- [ ] **Collect real iTerm2 logs** from current AI sessions
- [ ] **Document log format variations** across different AI interactions
- [ ] **Identify parsing challenges** from actual data
- [ ] **Create test fixtures** from anonymized log samples

### 3. Basic Log Parser (Priority 1)
- [ ] **Parse timestamp format**: `[18/07/2025, 14:18:42.700]`
- [ ] **Extract clean messages** from keystroke sequences
- [ ] **Handle editing patterns** (backspace, corrections)
- [ ] **Test with real log data**
- [ ] **integrate with zatso**

## Sprint 1: Core Infrastructure (Weeks 1-2)

### Sprint Goal
Build and test the foundational components with real iTerm2 logs.

### Deliverables
1. **Working log parser** that extracts clean messages
2. **File watcher system** monitoring log changes in real-time
3. **Basic hub coordinator** managing multiple channels
4. **CLI interface** for `maco watch` and `maco history`

### Tasks Breakdown

#### Week 1: Log Parser + File Watcher
```python
# Target API for Week 1
from maco.log_parser import parse_iterm_log
from maco.watcher import LogWatcher

# Parse existing log file
messages = parse_iterm_log("~/log/20250718_141841.Claude.log")
print(f"Found {len(messages)} complete messages")

# Watch for new messages
watcher = LogWatcher("~/log/")
watcher.on_new_message(lambda msg: print(f"New: {msg.content}"))
watcher.start()
```

#### Week 2: Hub Coordinator + CLI
```bash
# Target CLI for Week 2
maco watch ~/log/                    # Start monitoring
maco history "parser" --channel claude  # Search messages
maco channels                        # List active channels
```

### Success Criteria
- [ ] **Parse real logs**: Successfully extract messages from actual iTerm2 sessions
- [ ] **Real-time monitoring**: Detect new messages within 1-2 seconds
- [ ] **Multi-channel support**: Track Claude, Gemini, rovodev separately
- [ ] **Basic search**: Find messages by keyword and channel

## Sprint 2: Broadcasting & Integration (Weeks 3-4)

### Sprint Goal
Implement message broadcasting to AI panes and Python API integration.

### Deliverables
1. **Broadcasting system** sending messages to specific iTerm2 panes
2. **Python API** for programmatic hub interaction
3. **Configuration system** using pysyte patterns
4. **Integration tests** with actual multi-AI scenarios

### Key Features
```python
# Target API for Sprint 2
from maco import hub

# Send to specific AI
hub.say("Review this code", channel="claude")

# Broadcast to all AIs
hub.broadcast("Let's discuss the architecture")

# Listen for responses
@hub.on_message("gemini")
def handle_gemini(sender, content, timestamp):
    print(f"Gemini says: {content}")
```

### Technical Challenges
- **iTerm2 automation**: AppleScript integration for message injection
- **Message correlation**: Link broadcasts with AI responses
- **Pane identification**: Map channels to specific iTerm2 panes
- **Error handling**: Graceful failure when AIs are offline

## Sprint 3: Production Ready (Weeks 5-6)

### Sprint Goal
Polish for real-world usage and prepare for distribution.

### Deliverables
1. **Conversation management** with threading and context preservation
2. **Advanced search** with semantic capabilities
3. **Performance optimization** for long development sessions
4. **Documentation completion** and tutorial creation

### Production Features
- **Session persistence**: Save/restore conversation state
- **Export functionality**: Generate session reports and summaries
- **Plugin architecture**: Support for additional AI assistants
- **Performance monitoring**: Track resource usage and optimization

## Dependencies & Prerequisites

### External Dependencies
- **iTerm2**: Session logging must be configured and working
- **Python 3.13+**: For async/await and modern type hints
- **macOS**: Required for iTerm2 automation

### Internal Dependencies
- **pysyte**: Configuration discovery and path utilities
- **pym**: Visitor patterns for structured parsing
- **zatso**: Bi-directional parsing for complex log formats
- **crumbcutter**: Project scaffolding and structure

### Setup Requirements
```bash
# Verify iTerm2 logging
ls ~/log/*.log  # Should show recent AI session logs

# Check Python environment
python --version  # Should be 3.13+
pip list | grep -E "(pysyte|pym|zatso)"  # Verify dependencies

# Confirm iTerm2 automation access
osascript -e 'tell application "iTerm2" to get name of every session of current window'
```

## Resource Allocation

### Time Estimates
- **Sprint 1**: 15-20 hours (core infrastructure)
- **Sprint 2**: 12-15 hours (broadcasting and API)
- **Sprint 3**: 10-12 hours (polish and optimization)
- **Total**: ~40 hours over 6 weeks

### Effort Distribution
- **60% Implementation**: Core features and functionality
- **25% Testing**: Unit tests, integration tests, dogfooding
- **15% Documentation**: Updates to README, CLAUDE.md, examples

### Critical Path
1. **Log Parser** → File Watcher → Hub Coordinator
2. **Broadcasting** → Python API → Configuration
3. **Integration** → Testing → Documentation

## Risk Mitigation

### Technical Risks
- **iTerm2 API limitations**: Fallback to manual copying if automation fails
- **Log format changes**: Build flexible parser with version detection
- **Performance issues**: Implement caching and efficient file monitoring

### Schedule Risks
- **Complexity underestimation**: Focus on MVP features first
- **Integration challenges**: Test with real usage scenarios early
- **Dependency delays**: Have fallback implementations ready

## Success Metrics

### Sprint 1 Success
- [ ] Parse 100+ real messages from existing logs without errors
- [ ] Detect new messages in under 2 seconds
- [ ] Successfully distinguish between 3+ AI channels

### Sprint 2 Success
- [ ] Successfully broadcast message to specific iTerm2 pane
- [ ] Complete Python API covers 80% of common use cases
- [ ] Configuration system works with existing pysyte patterns

### Sprint 3 Success
- [ ] Complete 8-hour development session using maco exclusively
- [ ] Generate meaningful conversation summary/export
- [ ] Performance acceptable for sessions with 500+ messages

### Overall Project Success
- [ ] **Dogfooding**: Develop a significant feature using maco coordination
- [ ] **Multi-AI coordination**: Successfully coordinate Claude/Gemini/rovodev
- [ ] **Workflow improvement**: Measurable reduction in context switching
- [ ] **Distribution ready**: Package installable via `pip install macos`

## Sprint 4: Enhanced Architecture (Future Vision)

### Sprint Goal
Extend maco with structured conversation channels and knowledge extraction capabilities.

### Strategic Vision
*See `architecture.md` for comprehensive design rationale and technical decisions.*

### Deliverables
1. **Directory-Based Conversation Channels**
   - Structured hub organization (`./hub/{project}/{topic}/{participant}.md`)
   - Git-versioned conversation history
   - Asynchronous file-based communication
   - Reduced typo visibility with vim-based editing

2. **Rich Data Source MCP**
   - Transform conversation files into structured knowledge
   - Cross-file conversation threading and context extraction
   - Problem-solution pattern recognition and mapping
   - Decision tracking with reasoning chains
   - Searchable knowledge base for AI consumption

3. **"Conversation as Code" Patterns**
   - Versionable AI-human collaboration workflows
   - Cross-project knowledge sharing
   - Reusable conversation patterns and templates

### Integration with Core maco
- **Extends** File Watcher to monitor `./hub/` directories
- **Enhances** Conversation Manager with file-based persistence
- **Adds** MCP layer for knowledge extraction
- **Maintains** existing iTerm2 real-time capabilities

### Success Criteria
- [ ] **Directory channels working**: Write-process-git-wipe cycle functional
- [ ] **Knowledge extraction**: MCP identifies problem-solution patterns
- [ ] **Cross-project value**: Hub conversations benefit multiple projects
- [ ] **Async collaboration**: Effective vim-based conversation editing

## Next Actions

### Immediate (Today)
1. **Collect sample logs** from current AI sessions
2. **Set up development environment** with proper dependencies
3. **Create initial project structure** using crumbcutter

### This Week
1. **Implement basic log parser** with real data
2. **Test file watching** with live iTerm2 sessions
3. **Design hub coordinator** architecture

### Next Sprint Planning
1. **Review Sprint 1 deliverables** and adjust timeline
2. **Plan broadcasting implementation** based on iTerm2 research
3. **Define integration test scenarios** for multi-AI workflows

---

*This plan will be updated as development progresses and new requirements emerge.*
