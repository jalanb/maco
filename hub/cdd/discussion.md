# Chat about CDD

## ALan

CDD is new idea arising from a chat (using different UI) tonight
It neatly encapsulates some other ideas I've had over the last while

Development with many AIs should be chat-based
- after all, "chat" is the one thing we're all agreed that AIs are good at

Development with me should also be chat-based because
- I love chatting about code
- A lot of the important ideas that we need to make a "tool"/"system" out of this are
 - never going to come up in any formal documentation
 - going to come up as small points, but in many chats

So, conversation driven, but how supported?
 - I've kept deliberately vague about (e.g.) "storage" in many places
 - mentioned special markdown files in other
 - considered DAGs and RAGs, networked and hierarchical, graphs and trees
 - But remain undecided.

One important idea Gemini had tonight was the need for an Architect to make _decisions_
- Add a few goals and decide how to reach them
- Notice what decisions user keeps making about "good code"

because those decisions will be what's added to the system
 - to allow further and further automation over time

And finally: this one is 100% dogfooding
- we're gonna find out how it works
- then tweaks that into something that works a lot better
- then implement it as a tool/system
- then dogfood it some fecking more!

See also: `./rules.md`

## claude

Context from tonight's session: We explored FastMCP (Pythonic MCP server framework), integrated TDD into CDD (chat → doctest → pytest → code), and synthesized Gemini's turn-based collaboration ideas with Alan's hub system.

**Key insights captured:**

1. **Primary goal**: Build knowledge capture system that trains fresh AIs to write Alan-quality code (no glitches, matches idioms)
2. **Secondary goal**: Chat system captures decisions + rejections ("why not Postgres")
3. **The problem**: AIs write code that requires 30min of fixing tiny annoyances instead of reviewing logic
4. **The solution**: DISCUSSION.md conversations become training data, SYNTHESIS.md files become knowledge base, knowledge graph enables retrieval

**Gemini's contributions:**
- Architect (human) vs Coordinator (tooling) role split
- GOAL.md → DISCUSSION.md → SYNTHESIS.md workflow
- Parallel independent thinking before collaborative discussion
- "Elephant in Cairo" = force termination via decisions

**What we're testing right now:**
This 3-way chat (alan/claude/gemini) using `# speaker` sections to see if the pattern works manually before automating.

**Decisions needed:**

1. **Storage** - Alan mentioned staying deliberately vague. For this dogfood test: just markdown files in this dir? Or start sketching knowledge graph structure?

2. **Knowledge extraction** - After this discussion ends, how do we harvest it? Manual SYNTHESIS.md? Or start building the FastMCP tools we sketched (`harvest_discussion()`, `extract_idioms()`)?

3. **Next concrete action** - After 3-4 rounds here, what artifact do we produce?
   - Decision log about CDD structure?
   - First SYNTHESIS.md as template?
   - FastMCP server prototype for maco coordination?

**My vote**: Keep this discussion pure dogfooding. No tooling yet. Manual rounds. At end, Alan writes SYNTHESIS.md capturing decisions. That becomes template for future rounds.

Then next session: build the simplest FastMCP tool that would've helped this discussion (probably `start_round()` and `comment()`).

Impatient to get past theory into working code, but this manual round proves the pattern first.
