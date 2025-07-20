# maco Enhanced Architecture

## Executive Summary

This document describes the strategic architecture for extending maco beyond real-time iTerm2 log monitoring to include structured, git-versioned conversation channels and knowledge extraction capabilities. The enhanced architecture enables "conversation as code" development patterns while maintaining full compatibility with existing iTerm2 workflows.

## System Architecture

### Component Overview

```
┌─────────────────────┐    ┌─────────────────────┐    ┌─────────────────────┐
│   iTerm2 Logs       │    │  Directory Channels │    │   Rich Data MCP     │
│                     │    │                     │    │                     │
│ • Real-time         │    │ • Structured files  │    │ • Knowledge base    │
│ • Keystroke capture │    │ • Git versioned     │    │ • Pattern matching  │
│ • Multi-AI panes    │    │ • Async editing     │    │ • Decision tracking │
└─────────┬───────────┘    └─────────┬───────────┘    └─────────┬───────────┘
          │                          │                          │
          ▼                          ▼                          ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           maco Core Hub                                     │
│                                                                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐             │
│  │  Log Parser     │  │ Directory       │  │ Conversation    │             │
│  │                 │  │ Watcher         │  │ Manager         │             │
│  │ • Keystroke     │  │                 │  │                 │             │
│  │   analysis      │  │ • File change   │  │ • Thread        │             │
│  │ • Message       │  │   monitoring    │  │   management    │             │
│  │   extraction    │  │ • Git workflow  │  │ • Cross-file    │             │
│  │                 │  │   integration   │  │   linking       │             │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘             │
│                                                                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐             │
│  │  Broadcaster    │  │ Hub Coordinator │  │ Knowledge       │             │
│  │                 │  │                 │  │ Extractor       │             │
│  │ • AI pane       │  │ • Channel       │  │                 │             │
│  │   targeting     │  │   routing       │  │ • Problem-      │             │
│  │ • Message       │  │ • Message       │  │   solution      │             │
│  │   injection     │  │   distribution  │  │   mapping       │             │
│  │                 │  │ • State mgmt    │  │ • Context       │             │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Data Flow Architecture

#### Real-Time Flow (Current)
```
User Input → iTerm2 Pane → Log File → Log Parser → Hub Coordinator → Broadcaster → AI Panes
```

#### Directory-Based Flow (Enhanced) 
```
Write Response → ./hub/{channel}/{participant}.md → Directory Watcher → Process File → UI Display
                                                   ↓
Git Branch → Review → Wipe File → Ready for Next Response
```

#### Knowledge Extraction Flow (Advanced)
```
Both Flows → Rich Data MCP → Problem-Solution Mapping → Knowledge Base → AI Consumption
           ↓                                           ↓
Cross-File Threading → Context Extraction → Decision Tracking → Reusable Patterns
```

## Technical Decision Records

### TDR-001: Directory-Based Channel Structure

**Decision**: Use filesystem directories to organize conversations by project/topic/participant.

**Rationale**:
- **Familiar paradigm**: Developers understand directories and files
- **Git integration**: Natural fit with existing version control workflows  
- **Scalability**: Easy to add new projects, topics, or participants
- **Tool compatibility**: Works with vim, grep, find, and other Unix tools
- **Backup/sync**: Standard filesystem tools handle persistence

**Structure**:
```
./hub/
├── general/                    # Cross-project discussions
├── pysyte/                    # Project-specific channels
│   ├── trees/                 # Feature-specific threads  
│   │   ├── claude.md         # AI responses
│   │   ├── gemini.md         # AI responses
│   │   └── jalanb.md         # Human responses
│   └── root_docs/            # Documentation discussions
└── crumbcutter/              # Other project channels
```

**Alternatives Considered**:
- Database storage (rejected: adds complexity, reduces transparency)
- Single file with sections (rejected: merge conflicts, editing complexity)
- JSON/YAML format (rejected: less human-readable than Markdown)

### TDR-002: Git-Based Conversation Versioning

**Decision**: Use git branches for conversation state management with wipe-and-reset workflow.

**Rationale**:
- **Version history**: Full conversation evolution tracking
- **Conflict resolution**: Git's merge capabilities handle concurrent edits
- **Distributed collaboration**: Multiple developers can participate asynchronously
- **Backup and recovery**: Git's distributed nature provides resilience
- **Integration**: Fits existing development workflows

**Workflow**:
1. Write response to `{participant}.md`
2. Directory watcher detects change
3. Process file content for UI display
4. Stage changes to git branch
5. Wipe file clean for next response
6. Commit completed conversation threads

**Alternatives Considered**:
- File-based locking (rejected: doesn't handle conflicts well)
- Database transactions (rejected: adds infrastructure complexity)
- Append-only logs (rejected: difficult to edit/correct responses)

### TDR-003: Markdown with Quotation Standards

**Decision**: Use Markdown format with standardized quotation syntax for cross-references.

**Rationale**:
- **Human readable**: Easy to edit in vim or any text editor
- **Tool support**: Existing Markdown processors and syntax highlighting
- **Quotation capability**: Natural `> ` syntax for referencing other files/responses
- **Documentation fit**: Consistent with existing project documentation
- **AI parseable**: Structured enough for automated processing

**Quotation Standards**:
```markdown
# Reference other participant in same channel
> @claude said: "This approach makes sense"

# Reference other channel/topic
> From pysyte/trees/@jalanb: "The refactor is blocked by time"

# Reference external decision
> See architecture.md#TDR-002 for git workflow rationale
```

**Alternatives Considered**:
- JSON/YAML (rejected: not human-editable enough)
- Custom format (rejected: reinventing standards)
- Plain text (rejected: lacks structure for automated processing)

### TDR-004: MCP Integration Approach

**Decision**: Implement Rich Data Source as Model Context Protocol (MCP) server.

**Rationale**:
- **Standard interface**: MCP provides established patterns for AI tool integration
- **Bidirectional communication**: AIs can query and receive structured knowledge
- **Extensibility**: Easy to add new knowledge extraction capabilities
- **Performance**: Efficient data transfer compared to file parsing
- **Ecosystem fit**: Integrates with Claude's existing MCP support

**MCP Capabilities**:
- `get_conversation_history(project, topic, timeframe)`
- `find_problem_solutions(problem_description)`
- `track_decision_chain(decision_id)`
- `extract_conversation_patterns(participant_filter)`
- `generate_knowledge_summary(scope)`

**Alternatives Considered**:
- REST API (rejected: more complex, less integrated)
- File-based queries (rejected: slower, less structured)
- Database views (rejected: adds infrastructure dependency)

## Design Patterns

### "Conversation as Code" Philosophy

**Core Principle**: Treat AI-human conversations as versionable, reviewable, and reusable code artifacts.

**Implementation Patterns**:

#### 1. Conversation Branching
```
main conversation thread
├── alternative-approach/     # Explore different solution
│   ├── claude.md            # AI analysis of alternative
│   └── jalanb.md           # Human evaluation
└── implementation-details/   # Dive deeper into specifics
    ├── gemini.md           # Implementation suggestions
    └── rovodev.md          # Code review perspective
```

#### 2. Problem-Solution Templates
```markdown
## Problem Statement
**Context**: {background_information}
**Challenge**: {specific_issue}
**Constraints**: {limitations}

## Proposed Solutions
1. **Option A**: {description}
   - Pros: {advantages}
   - Cons: {disadvantages}
   - Effort: {time_estimate}

## Decision
**Chosen**: {selected_option}
**Rationale**: {reasoning}
**Next Steps**: {action_items}
```

#### 3. Knowledge Accumulation
```markdown
## Lessons Learned
- **Pattern**: Similar to {previous_project}#{topic}
- **Anti-pattern**: Avoid {problematic_approach} due to {reason}
- **Best practice**: Always {recommended_action} when {condition}

## Reusable Components
- Code: See {repository}#{commit}
- Documentation: See {file}#{section}
- Process: See {conversation}#{decision}
```

### Async vs Real-Time Communication Trade-offs

**Real-Time (iTerm2) - Best For**:
- Rapid prototyping and brainstorming
- Immediate feedback and clarification
- Live debugging sessions
- Quick status updates

**Async (Directory-Based) - Best For**:
- Thoughtful analysis and reflection
- Complex problem decomposition
- Cross-project knowledge sharing
- Formal decision documentation

**Integration Strategy**:
```python
# Automatic escalation from real-time to async
if conversation_length > threshold:
    hub.suggest_async_channel(topic=current_topic)

# Async summary back to real-time
if async_conversation.has_decision():
    hub.broadcast_summary(async_conversation.decision)
```

### Cross-Project Knowledge Sharing

**Hub Structure for Knowledge Sharing**:
```
./hub/
├── patterns/                  # Reusable conversation patterns
│   ├── problem-solving.md    # Template for structured problem analysis
│   ├── code-review.md        # Template for AI-assisted reviews
│   └── architecture.md       # Template for design discussions
├── knowledge-base/           # Accumulated insights
│   ├── common-solutions.md   # Frequently effective approaches
│   ├── anti-patterns.md      # Things to avoid
│   └── tool-integration.md   # How tools work together
└── decisions/                # Cross-project decision tracking
    ├── tech-stack.md         # Technology choices and rationale
    ├── conventions.md        # Coding and documentation standards
    └── processes.md          # Workflow and collaboration patterns
```

### Plugin Architecture for Extensibility

**Core Plugin Interface**:
```python
from abc import ABC, abstractmethod

class ConversationProcessor(ABC):
    @abstractmethod
    def can_process(self, file_path: str, content: str) -> bool:
        """Determine if this processor handles the content type."""
        pass
    
    @abstractmethod
    def extract_knowledge(self, content: str) -> Dict[str, Any]:
        """Extract structured knowledge from conversation content."""
        pass
    
    @abstractmethod
    def generate_summary(self, knowledge: Dict[str, Any]) -> str:
        """Generate human-readable summary of extracted knowledge."""
        pass

# Example: Code Review Processor
class CodeReviewProcessor(ConversationProcessor):
    def can_process(self, file_path: str, content: str) -> bool:
        return "code review" in content.lower() or "review:" in content
    
    def extract_knowledge(self, content: str) -> Dict[str, Any]:
        return {
            "files_reviewed": extract_file_references(content),
            "issues_found": extract_issue_patterns(content),
            "suggestions": extract_suggestions(content),
            "approval_status": determine_approval(content)
        }
```

## Data Models

### Conversation Threading Structure

```python
from dataclasses import dataclass
from datetime import datetime
from typing import List, Optional, Dict, Any

@dataclass
class ConversationMessage:
    participant: str          # "claude", "gemini", "jalanb", etc.
    content: str             # Message content
    timestamp: datetime      # When message was created
    file_path: str           # Source file location
    references: List[str]    # Quoted/referenced content
    metadata: Dict[str, Any] # Additional structured data

@dataclass
class ConversationThread:
    topic: str                        # "pysyte/trees", "general", etc.
    participants: List[str]           # Active participants
    messages: List[ConversationMessage] # Ordered message history
    created_at: datetime             # Thread start time
    last_activity: datetime          # Most recent message
    status: str                      # "active", "resolved", "archived"
    decision_points: List[str]       # Key decisions made
    knowledge_extracted: bool        # Whether MCP has processed

@dataclass
class ConversationContext:
    project: str                     # "pysyte", "crumbcutter", etc.
    related_threads: List[str]       # Connected conversation topics
    problem_domain: str              # "refactoring", "bug-fix", etc.
    solution_patterns: List[str]     # Identified solution approaches
    decision_chain: List[str]        # Sequence of related decisions
```

### Problem-Solution Mapping Schema

```python
@dataclass
class ProblemStatement:
    description: str              # Human-readable problem description
    context: Dict[str, Any]      # Background information and constraints
    domain: str                  # "technical", "process", "strategic"
    complexity: str              # "simple", "moderate", "complex"
    stakeholders: List[str]      # People/roles affected
    related_problems: List[str]  # Similar issues encountered before

@dataclass
class SolutionApproach:
    description: str             # Human-readable solution description
    implementation: str          # Technical approach or steps
    effort_estimate: str         # Time/complexity estimate
    pros: List[str]             # Advantages of this approach
    cons: List[str]             # Disadvantages or risks
    prerequisites: List[str]     # Required before implementation
    success_criteria: List[str]  # How to measure success

@dataclass
class ProblemSolutionMapping:
    problem: ProblemStatement
    solutions: List[SolutionApproach]
    chosen_solution: Optional[str]    # Which solution was selected
    decision_rationale: str           # Why this solution was chosen
    implementation_status: str        # "planned", "in-progress", "completed"
    lessons_learned: List[str]        # Insights gained from implementation
    reusability_score: float          # How applicable to other contexts
```

### Cross-Reference Resolution Algorithms

**Reference Detection Patterns**:
```python
import re
from typing import List, Dict, Optional

class ReferenceResolver:
    """Resolve cross-references in conversation content."""
    
    # Patterns for different reference types
    PARTICIPANT_REF = re.compile(r'@(\w+)\s+said:\s*["\'"](.*?)["\'"']', re.DOTALL)
    FILE_REF = re.compile(r'From\s+([^:]+):@(\w+):\s*["\'"](.*?)["\'"']', re.DOTALL)
    DOCUMENT_REF = re.compile(r'See\s+([^#]+)#([^#\s]+)(?:#(\S+))?')
    DECISION_REF = re.compile(r'Decision\s+([A-Z]+-\d+)')
    CODE_REF = re.compile(r'`([^`]+)`')
    
    def extract_references(self, content: str) -> Dict[str, List[str]]:
        """Extract all types of references from content."""
        return {
            'participants': self._extract_participant_refs(content),
            'files': self._extract_file_refs(content),
            'documents': self._extract_document_refs(content),
            'decisions': self._extract_decision_refs(content),
            'code': self._extract_code_refs(content)
        }
    
    def resolve_reference(self, ref_type: str, ref_content: str) -> Optional[str]:
        """Resolve a reference to its actual content/location."""
        resolvers = {
            'participants': self._resolve_participant_ref,
            'files': self._resolve_file_ref,
            'documents': self._resolve_document_ref,
            'decisions': self._resolve_decision_ref,
            'code': self._resolve_code_ref
        }
        resolver = resolvers.get(ref_type)
        return resolver(ref_content) if resolver else None
```

### Knowledge Extraction Pipelines

```python
from typing import Iterator, Any

class KnowledgeExtractionPipeline:
    """Process conversations through multiple extraction stages."""
    
    def __init__(self):
        self.processors = [
            ProblemIdentificationProcessor(),
            SolutionMappingProcessor(),
            DecisionTrackingProcessor(),
            PatternRecognitionProcessor(),
            ContextExtractionProcessor()
        ]
    
    def process_conversation(self, thread: ConversationThread) -> Dict[str, Any]:
        """Run conversation through all extraction processors."""
        knowledge = {}
        
        for processor in self.processors:
            try:
                extracted = processor.extract(thread)
                knowledge[processor.name] = extracted
            except Exception as e:
                # Log error but continue with other processors
                knowledge[processor.name] = {"error": str(e)}
        
        return knowledge
    
    def generate_insights(self, knowledge: Dict[str, Any]) -> List[str]:
        """Generate human-readable insights from extracted knowledge."""
        insights = []
        
        # Cross-processor analysis
        if 'problems' in knowledge and 'solutions' in knowledge:
            insights.extend(self._analyze_problem_solution_fit(
                knowledge['problems'], knowledge['solutions']
            ))
        
        if 'patterns' in knowledge:
            insights.extend(self._identify_recurring_patterns(
                knowledge['patterns']
            ))
        
        if 'decisions' in knowledge:
            insights.extend(self._track_decision_evolution(
                knowledge['decisions']
            ))
        
        return insights
```

## Integration Strategies

### With Existing pysyte/pym/zatso Ecosystem

**Configuration Discovery** (pysyte patterns):
```python
# Use pysyte's configuration discovery for maco settings
from pysyte.config.urator import find_config

maco_config = find_config("maco.yaml", search_parents=True)
hub_directories = maco_config.get("hub_directories", ["./hub"])
conversation_templates = maco_config.get("templates", {})
```

**Visitor Patterns** (pym integration):
```python
# Use pym's visitor patterns for conversation processing
from pym.visitors import Visitor

class ConversationAnalyzer(Visitor):
    def visit_message(self, message: ConversationMessage):
        # Analyze individual messages
        pass
    
    def visit_thread(self, thread: ConversationThread):
        # Analyze conversation threads
        pass
    
    def visit_decision(self, decision: DecisionPoint):
        # Track decision evolution
        pass
```

**Bi-directional Parsing** (zatso integration):
```python
# Use zatso for structured conversation templates
from zatso import Grammar

conversation_grammar = Grammar.from_file("conversation.ebnf")

# Parse conversation into structured data
structured_data = conversation_grammar.parse(conversation_content)

# Generate conversation from structured data
conversation_content = conversation_grammar.generate(structured_data)
```

### With crumbcutter Project Scaffolding

**Project Template Integration**:
```yaml
# crumbcutter template: project-with-hub.yaml
structure:
  - "README.md"
  - "CLAUDE.md"
  - "PLAN.md"
  - "architecture.md"
  - "hub/"
  - "hub/general/"
  - "hub/{{project_name}}/"
  - "hub/{{project_name}}/architecture/"
  - "hub/{{project_name}}/implementation/"

hub_config:
  participants: ["claude", "gemini", "rovodev", "{{author}}"]
  templates:
    problem_solving: "hub/templates/problem-solving.md"
    code_review: "hub/templates/code-review.md"
    architecture: "hub/templates/architecture.md"
```

**Automatic Hub Setup**:
```bash
# crumbcutter generates project with maco integration
cutr new my-project --template project-with-hub
cd my-project

# Automatically configure maco for this project
maco init --project my-project --participants claude,gemini,rovodev
```

### With External AI APIs (Future Expansion)

**Plugin Architecture for New AIs**:
```python
class AIAdapter(ABC):
    @abstractmethod
    def can_handle(self, ai_name: str) -> bool:
        """Determine if this adapter handles the AI."""
        pass
    
    @abstractmethod
    def send_message(self, message: str, context: Dict[str, Any]) -> str:
        """Send message to AI and return response."""
        pass
    
    @abstractmethod
    def get_capabilities(self) -> List[str]:
        """Return list of AI capabilities."""
        pass

# Example: Direct API integration
class OpenAIAdapter(AIAdapter):
    def send_message(self, message: str, context: Dict[str, Any]) -> str:
        # Direct API call instead of iTerm2 automation
        return openai.chat.completions.create(...)
```

### With Development Workflows

**Git Integration**:
```bash
# Automatic git hooks for conversation tracking
# .git/hooks/pre-commit
#!/bin/bash
# Process any pending hub conversations before commit
maco process-pending --channel all

# Generate conversation summary in commit message
maco summarize --since last-commit >> .git/COMMIT_EDITMSG
```

**IDE Integration** (VS Code extension concept):
```json
{
  "commands": [
    {
      "command": "maco.startConversation",
      "title": "Start maco Conversation",
      "category": "maco"
    },
    {
      "command": "maco.queryKnowledge",
      "title": "Query Conversation Knowledge",
      "category": "maco"
    }
  ],
  "views": {
    "explorer": [
      {
        "id": "macoConversations",
        "name": "Active Conversations",
        "when": "maco.enabled"
      }
    ]
  }
}
```

**Testing Integration**:
```python
# Test conversation patterns and knowledge extraction
def test_problem_solution_extraction():
    conversation = load_test_conversation("problem-solving-example.md")
    knowledge = extract_knowledge(conversation)
    
    assert "problem_statement" in knowledge
    assert "solutions" in knowledge
    assert len(knowledge["solutions"]) >= 2
    assert knowledge["chosen_solution"] is not None

def test_cross_reference_resolution():
    content = "See architecture.md#TDR-002 for rationale"
    refs = resolve_references(content)
    
    assert len(refs) == 1
    assert refs[0]["type"] == "document"
    assert refs[0]["file"] == "architecture.md"
    assert refs[0]["section"] == "TDR-002"
```

## Implementation Roadmap

### Phase 1: Foundation (Weeks 1-2)
- Directory structure creation and monitoring
- Basic git workflow integration
- Simple Markdown processing
- File wipe-and-reset cycle

### Phase 2: Knowledge Extraction (Weeks 3-4)  
- MCP server implementation
- Problem-solution pattern recognition
- Cross-reference resolution
- Basic knowledge querying

### Phase 3: Advanced Features (Weeks 5-6)
- Template system for conversation patterns
- Advanced knowledge insights
- Cross-project knowledge sharing
- Performance optimization

### Phase 4: Ecosystem Integration (Weeks 7-8)
- pysyte/pym/zatso integration
- crumbcutter template integration  
- IDE plugins and workflow automation
- Documentation and tutorials

## Success Metrics

### Technical Metrics
- **Response time**: Directory processing < 500ms
- **Storage efficiency**: Conversations compress 80%+ in git
- **Knowledge accuracy**: 90%+ precision in problem-solution matching
- **Cross-reference resolution**: 95%+ successful link resolution

### User Experience Metrics
- **Adoption rate**: 80%+ of conversations use directory channels within 1 month
- **Context preservation**: Users report improved conversation continuity
- **Knowledge reuse**: 50%+ of new problems find relevant historical solutions
- **Workflow integration**: Seamless git/IDE integration reported by users

### Business Impact Metrics
- **Development velocity**: Measurable reduction in context switching time
- **Knowledge retention**: Reduced time to onboard new team members
- **Decision quality**: Better documented and justified technical decisions
- **Collaboration effectiveness**: Improved multi-AI coordination outcomes

---

*This architecture document will evolve as implementation progresses and new requirements emerge through dogfooding and user feedback.*