# Maco Orchestration Implementation Strategy

## Planning Mode: On

The 14-step algorithm needs concrete implementation. Breaking down the technical requirements.

## Core Orchestration Components

**File System Watcher:**
```python
# inotify-based monitoring preferred over polling
from watchdog import Observer, FileSystemEventHandler

class HubWatcher(FileSystemEventHandler):
    def on_modified(self, event):
        if event.src_path.endswith('/UPPER.md'):
            self.check_round_completion()
```

**Round Coordinator:**
- Detect when all participants have written files
- Archive UPPER.md files to SQLite database  
- Clear files for next round
- Generate final HUB.md when convergence reached

**AI Invitation System:**
- Queue-based with configurable team order
- Timeout handling for non-responsive AIs
- Graceful degradation and retry logic

## Technical Decisions

**Database Schema:**
```sql
CREATE TABLE rounds (
    id INTEGER PRIMARY KEY,
    hub_path TEXT,
    round_number INTEGER,
    participant TEXT,
    content TEXT,
    timestamp DATETIME
);
```

**Error Handling:**
- AI timeout: Continue with available responses
- File corruption: Restore from previous round  
- System crash: Resume from database state

## Integration Points

**With existing maco architecture:**
- Leverage iTerm2 log parsing for AI communication
- Build on chat/UI foundations when they exist
- Use pysyte patterns for configuration discovery

**With hub system:**
- Monitor multiple hub directories simultaneously
- Handle nested hub structures (like jalanb/hub/hub/)
- Coordinate with git-based conversation versioning

## Implementation Questions

**Gold - Need clarity:**
1. Which AI invitation protocol? (iTerm2 panes vs direct file writes)
2. Where does orchestration run? (background daemon vs on-demand)
3. How do we bootstrap the first maco hub conversation?

**Silver - Implementation details:**
4. SQLite file location and backup strategy?
5. Timeout values for different AIs?
6. Integration with existing `gc` git helpers?

## MVP Scope

**Phase 1 (Next week):**
- Basic file watching for single hub
- Manual round coordination (no automation)
- Simple UPPER.md archival to files (not database)

**Phase 2 (Following week):**
- Multi-hub monitoring
- Automated round detection and clearing
- SQLite integration for round history

**Phase 3 (Future):**
- AI invitation automation
- HUB.md narrative generation
- Integration with pysyte ecosystem

## Dogfooding Strategy

**Use this exact hub system to develop maco:**
- Each implementation decision gets discussed in maco/hub/
- Round-based architecture review before coding
- Real-world testing of the orchestration algorithms

The meta-recursion of using hubs to build hub tooling is perfect validation.

Ready to begin Phase 1 implementation.