# Goals

A goal should be
- clear
- precise
- needed
- actionable

## alan

1. DefineStorage

We need a far better grasp of "how to store" knowledge
- from vague philosophies to crisp assignments
- and all their relationships and contexts

2. MVP MCP

The only code worth writing now is a "MCP" server framework in Python

2.1 offer read access to dir listings under /opt/clones/github/jalanb
2.2 take "proposed text" from AI, pre-process it, show to user
2.3 help user compose reply
2.5 pass reply back to AI

3. Build knowledge capture system that trains fresh AIs to write Alan-quality code
4. Chat system captures decisions + rejections ("why not Postgres")
4.1 System captures knowledge

## claude

**Re: Goal 1 (DefineStorage)**

From tonight's exploration, storage has 3 layers:

1. **Workspace layer** - discussion.md files (ephemeral, trim aggressively)
2. **Knowledge layer** - concept files extracted from discussions (persistent, queryable)
3. **Archive layer** - git history (full context, searchable)

Concrete next step: Create `concepts/` dir, extract first concept file from this discussion (maybe `concepts/cdd-workflow.md`?)

**Re: Goal 2 (MVP MCP)**

FastMCP server with 3 tools matches your spec:

```python
@mcp.tool()
def list_projects() -> list[str]:
    """List directories under /opt/clones/github/jalanb"""

@mcp.tool()
def preprocess_ai_text(text: str, context: str) -> str:
    """Lint/enhance AI output before showing to user"""
    # Check for smells, inject citations, etc

@mcp.tool()
def compose_reply(user_input: str) -> str:
    """Help user compose reply with relevant context"""
    # Query concept files for relevant decisions
```

This is buildable in next session.

**Re: Goals 3 & 4**

These are the long-term vision. Goals 1 & 2 are the path to get there.

**Missing goal:**

5. **Test the pattern** - Run 3-5 rounds of manual CDD, extract learnings before building automation
