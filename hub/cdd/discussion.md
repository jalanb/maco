# Chat about CDD

## ALan

CDD is new idea arising from a chat 
It encapsulates many important idea

Development with many AIs should be chat-based

Development with me should also be chat-based because 
- many good ideas are small but mentioned often

We need an _Architect_ to make _Decisions_
- Add a few goals and decide how to reach them
- Notice what decisions user keeps making about "good code"

because those decisions will be what's added to the system
 - to allow further and further automation over time

And finally: this one is 100% dogfooding

## Cittations

- ./rules.md

## claude

- FastMCP
- CDD based on TDD


Given: AIs write code that requires 30min of fixing tiny annoyances instead of reviewing logic
Then: 
- discussion.md becomes training data
- synthesis.md become knowledge base
- knowledge graph enables retrieval

Architect (human) vs Coordinator (tooling)

goal.md → discussion.md → synthesis.md workflow

- Parallel independent thinking before collaborative discussion

**Decisions needed:**

2. **Knowledge extraction** - After this discussion ends, how do we harvest it? Manual SYNTHESIS.md? Or start building the FastMCP tools we sketched (`harvest_discussion()`, `extract_idioms()`)?

**My vote**: Keep this discussion pure dogfooding. No tooling yet. Manual rounds. At end, Alan writes SYNTHESIS.md capturing decisions. That becomes template for future rounds.

next : build the simplest FastMCP tool that would've helped this discussion (probably `start_round()` and `comment()`).


## gemini


start thinking about **linkability** from day one.

A decision doesn't exist in a vacuum; it's part of a chain of reasoning.

final point in the synthesis could be: "**Next Action:** Build a FastMCP server with a single tool"
