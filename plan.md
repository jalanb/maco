# maco Development Plan

## Executive Summary


__Timeline__: 3 development sprints (2-3 weeks each)
__Success Metric__: Successfully coordinate a multi-AI development session using maco

## Immediate Next Steps (This Week)

```bash
# Use crumbcutter for project scaffolding
cd /opt/clones/github/jalanb/crumbs/crumbcutter
cutr new maco  # Generate project structure

# Set up development environment
cd /opt/clones/github/jalanb/macos/maco
pip install -e .
```

- [ ] __Parse timestamp format__: `[18/07/2025, 14:18:42.700]`
- [ ] __Extract clean messages__ from keystroke sequences
- [ ] __Handle editing patterns__ (backspace, corrections)
- [ ] __Test with real log data__
- [ ] __integrate with zatso__

## Sprint 1: Core Infrastructure (Weeks 1-2)

### Sprint Goal
Build and test the foundational components with real iTerm2 logs.

### Deliverables
1. __Working log parser__ that extracts clean messages
2. __File watcher system__ monitoring log changes in real-time
3. __Basic hub coordinator__ managing multiple channels
4. __CLI interface__ for `maco watch` and `maco history`

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
- [ ] __Parse real logs__: Successfully extract messages from actual iTerm2 sessions
- [ ] __Real-time monitoring__: Detect new messages within 1-2 seconds
- [ ] __Multi-channel support__: Track Claude, Gemini, rovodev separately
- [ ] __Basic search__: Find messages by keyword and channel

## Sprint 2: Broadcasting & Integration (Weeks 3-4)

### Sprint Goal
Implement message broadcasting to AI panes and Python API integration.

### Deliverables
1. __Broadcasting system__ sending messages to specific iTerm2 panes
2. __Python API__ for programmatic hub interaction
3. __Configuration system__ using pysyte patterns
4. __Integration tests__ with actual multi-AI scenarios

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
- __iTerm2 automation__: AppleScript integration for message injection
- __Message correlation__: Link broadcasts with AI responses
- __Pane identification__: Map channels to specific iTerm2 panes
- __Error handling__: Graceful failure when AIs are offline

## Sprint 3: Production Ready (Weeks 5-6)

### Sprint Goal
Polish for real-world usage and prepare for distribution.

### Deliverables
1. __Conversation management__ with threading and context preservation
2. __Advanced search__ with semantic capabilities
3. __Performance optimization__ for long development sessions
4. __Documentation completion__ and tutorial creation

### Production Features
- __Session persistence__: Save/restore conversation state
- __Export functionality__: Generate session reports and summaries
- __Plugin architecture__: Support for additional AI assistants
- __Performance monitoring__: Track resource usage and optimization

## Dependencies & Prerequisites

### External Dependencies
- __iTerm2__: Session logging must be configured and working
- __Python 3.13+__: For async/await and modern type hints
- __macOS__: Required for iTerm2 automation

### Internal Dependencies
- __pysyte__: Configuration discovery and path utilities
- __pym__: Visitor patterns for structured parsing
- __zatso__: Bi-directional parsing for complex log formats
- __crumbcutter__: Project scaffolding and structure

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
- __Sprint 1__: 15-20 hours (core infrastructure)
- __Sprint 2__: 12-15 hours (broadcasting and API)
- __Sprint 3__: 10-12 hours (polish and optimization)
- __Total__: ~40 hours over 6 weeks

### Effort Distribution
- __60% Implementation__: Core features and functionality
- __25% Testing__: Unit tests, integration tests, dogfooding
- __15% Documentation__: Updates to README, CLAUDE.md, examples

### Critical Path
1. __Log Parser__ → File Watcher → Hub Coordinator
2. __Broadcasting__ → Python API → Configuration
3. __Integration__ → Testing → Documentation

## Risk Mitigation

### Technical Risks
- __iTerm2 API limitations__: Fallback to manual copying if automation fails
- __Log format changes__: Build flexible parser with version detection
- __Performance issues__: Implement caching and efficient file monitoring

### Schedule Risks
- __Complexity underestimation__: Focus on MVP features first
- __Integration challenges__: Test with real usage scenarios early
- __Dependency delays__: Have fallback implementations ready

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
- [ ] __Dogfooding__: Develop a significant feature using maco coordination
- [ ] __Multi-AI coordination__: Successfully coordinate Claude/Gemini/rovodev
- [ ] __Workflow improvement__: Measurable reduction in context switching
- [ ] __Distribution ready__: Package installable via `pip install macos`

## Sprint 4: Enhanced Architecture (Future Vision)

### Sprint Goal
Extend maco with structured conversation channels and knowledge extraction capabilities.

### Strategic Vision
*See `architecture.md` for comprehensive design rationale and technical decisions.*

### Deliverables
1. __Directory-Based Conversation Channels__
   - Structured hub organization (`./hub/{project}/{topic}/{participant}.md`)
   - Git-versioned conversation history
   - Asynchronous file-based communication
   - Reduced typo visibility with vim-based editing

2. __Rich Data Source MCP__
   - Transform conversation files into structured knowledge
   - Cross-file conversation threading and context extraction
   - Problem-solution pattern recognition and mapping
   - Decision tracking with reasoning chains
   - Searchable knowledge base for AI consumption

3. __"Conversation as Code" Patterns__
   - Versionable AI-human collaboration workflows
   - Cross-project knowledge sharing
   - Reusable conversation patterns and templates

### Integration with Core maco
- __Extends__ File Watcher to monitor `./hub/` directories
- __Enhances__ Conversation Manager with file-based persistence
- __Adds__ MCP layer for knowledge extraction
- __Maintains__ existing iTerm2 real-time capabilities

### Success Criteria
- [ ] __Directory channels working__: Write-process-git-wipe cycle functional
- [ ] __Knowledge extraction__: MCP identifies problem-solution patterns
- [ ] __Cross-project value__: Hub conversations benefit multiple projects
- [ ] __Async collaboration__: Effective vim-based conversation editing

## Next Actions

### Immediate (Today)
1. __Collect sample logs__ from current AI sessions
2. __Set up development environment__ with proper dependencies
3. __Create initial project structure__ using crumbcutter

### This Week
1. __Implement basic log parser__ with real data
2. __Test file watching__ with live iTerm2 sessions
3. __Design hub coordinator__ architecture

### Next Sprint Planning
1. __Review Sprint 1 deliverables__ and adjust timeline
2. __Plan broadcasting implementation__ based on iTerm2 research

---

*This plan will be updated as development progresses and new requirements emerge.*
