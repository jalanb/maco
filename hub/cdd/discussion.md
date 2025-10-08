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

I'm guessing our primary artefacts should look like source code
- You know, good old `*.sh` and `*.py`
- And increasingly these days: `*.md`
- maybe a `pyproject.toml`

That sort of stuff should be the primary aim
- and including `*.md` affords a range of secondary aims

What is a `SYNTHESIS.md` when it's at home?

> FastMCP server prototype

Yes please - that should be a goal for ASAP

/


**My vote**: Keep this discussion pure dogfooding. No tooling yet. Manual rounds. At end, Alan writes SYNTHESIS.md capturing decisions. That becomes template for future rounds.

next : build the simplest FastMCP tool that would've helped this discussion (probably `start_round()` and `comment()`).


## gemini


start thinking about **linkability** from day one.

A decision doesn't exist in a vacuum; it's part of a chain of reasoning.


## alan

OK, I see what you want from me for a `synthesis.md` file.

And I'm up for a manual process for Round 1.
But I doubt I'll even last till Round 2.

Anyway, what do we think it should contain?

Is it just a big dictionary, keyed on words that turned up in the chat
- where "word" is interesting in some way

Or a more complicated data structure?
- thoughts?

### Git

I was lucky enough to remember that we were in a repo
- so I did a `git add` after each contribution
- and git a commit message from each of you for what you said
 - which becomes a lovely little summary of what was said

Unfortunately I did not see the possibilities of doing that for my own (starting) commit message
- so mine is boring, I'll be better next time

But now - we get a free history of the chat
- and if we were to need to show it as "turns" in some UI
- easy peasy

Also - because we got full history in git
- it's always easy to delete old text in the file

### Dogfooding

I do like this way of chatting
- I get to use `vim` which is just so much easier
- especially when I have to find a word

Also I see the "commenting syntax" is working well
- hence: this final section is also easier
- I don;t have to fill it with references to earlier text

### OMGit!

We synthesize from old text!

What we might do:
- everyone gets a turn to write
- after writing: "git add .; git commit -m '...'"
- archtitect reads all files
 - deletes as much text as he can, by
  - summarising
  - defining
  - linking
  - citing
  - Engineer-splaining
 - synthesizes as much knowledge from what's left
  - saves knowledge in the chat
  - and, maybe, in "The Knowledge Base"
- every one gets a turn again
- archtitect trims the fat
- round we go until:
 - there are no more entries in the git log since last time archtect was there

Comments? Critiques? Suggestions?

Special bonus points for anyone spotting a missing affordance :-)

Since I've had the idea about using git while editing this file
- I will save this to a backup
- Re-edit the file, and do my deleting bit
- git commit that
- come back here and say:


OK, did that.

```bash
commit e7f887f9ec6330bf80da1ee0689c6beb6a893071 (HEAD -> __main__)
Author: jalanb <github@al-got-rhythm.net>
Date:   Wed Oct 8 04:41:48 2025 +0100

    Alan: Squish context

 hub/cdd/discussion.md | 77 +++++++++++++++++++++++------------------------------------------------------
 hub/cdd/goals.md      | 28 ++++++++++++++++++++++++++++
 hub/cdd/rules.md      | 11 -----------
 hub/cdd/wish.md       |  9 +++------
 4 files changed, 54 insertions(+), 71 deletions(-)

commit c58daa71d7ebd0564898387ad2090e7901b906f8
Author: jalanb <github@al-got-rhythm.net>
Date:   Wed Oct 8 02:59:08 2025 +0100

    Gemini: Refine CDD procedure with linkability and parallel experiment

    Contribute to the first round of the CDD dogfooding session.

    - Agree with the manual, procedure-first approach
    - Emphasize the importance of "linkability" between decision artifacts, even in the manual stage, to set the foundation for a future knowledge graph.
    - Reinforce that the Architect's manual `SYNTHESIS.md` is the critical "elephant-placing" step and will serve as the golden-standard test case for future aut>
    - Propose an experiment for Round 2 to test the "parallel independent thinking" model.
    - Update `rules.md` to include the proposed procedure for the Round 2 experiment.

 hub/cdd/discussion.md | 18 ++++++++++++++++++
 hub/cdd/rules.md      |  7 +++++++
 2 files changed, 25 insertions(+)

commit 3b7063aab797a79054c4ab69027b571e1f2ad7d0
Author: jalanb <github@al-got-rhythm.net>
Date:   Wed Oct 8 02:39:28 2025 +0100

    Claude: Enhance CDD hub with Claude's synthesis of tonight's session

    Add Claude's perspective capturing:
    - Core CDD goals (knowledge capture → fresh AI training)
    - Integration of TDD workflow (chat → doctest → pytest)
    - Gemini's turn-based collaboration framework
    - Concrete definition of "code smell" prevention
    - JIT context delivery mechanism design

    Capture decisions needed for next steps and vote for manual dogfooding before tooling.

 hub/cdd/discussion.md | 37 +++++++++++++++++++++++++++++++++++++
 hub/cdd/rules.md      |  8 ++++----
 hub/cdd/wish.md       | 27 +++++++++++++++++++++++++++
 3 files changed, 68 insertions(+), 4 deletions(-)

commit c570d6bc7d2bbaa29ffe63ab1ea9d3818d502789
Author: jalanb <github@al-got-rhythm.net>
Date:   Wed Oct 8 02:30:15 2025 +0100

    Alan: start a chat about CDD

 hub/cdd/discussion.md | 36 ++++++++++++++++++++++++++++++++++++
 hub/cdd/rules.md      | 28 ++++++++++++++++++++++++++++
 hub/cdd/wish.md       | 20 ++++++++++++++++++++
 3 files changed, 84 insertions(+)

```

All I really did was compress/reduce `discussion.md` (and others)

And in doing so I wanted to ask:
- what is `synthesis.md` affording us that a well-trimmed `discussion.md` doesn't?
- as long as I keep going back, trimming away the fat
- reducing the noise, revealing signal

Then what we end up with is a very simple introduction
- all of which id highly relevant to the rest of the discussion
- and leads into the latest discussion

And the introduction may be simple
- but I don't see that it can't have everything that synthesis.md might have

Open to ideas on this one
- maybe `synthesis.md` affords something else?

## claude

**Re: synthesis.md vs trimmed discussion.md**

You're right - the git-backed trimming approach IS a form of synthesis. The question is: what's the artifact we query later?

**Option 1: Keep discussion.md, trim continuously**
- Pro: Single source of truth, git history preserves full context
- Pro: Natural evolution through editing
- Con: File grows unbounded (even trimmed, it accumulates)
- Con: Hard to query "what did we decide about storage?" without reading whole file

**Option 2: Extract synthesis.md from discussion.md**
- Pro: Clean decision artifact ("We chose X, rejected Y because Z")
- Pro: Queryable - one file per decision/topic
- Pro: Templates for FastMCP tools to extract
- Con: Duplication - decision exists in both files

**Option 3: Hybrid - discussion.md + concept files**
From knowledge-graph.md pattern:
```
hub/cdd/
  discussion.md       # Live chat, gets trimmed
  concepts/
    storage.md        # Extracted: all storage decisions
    mcp-server.md     # Extracted: MCP design decisions
```

**My vote: Option 3**

discussion.md is the workspace - trim it aggressively
Concept files are the knowledge base - extract when decisions solidify

This matches the `*concept*` pattern from knowledge-graph.md and gives us queryable artifacts without duplicating everything.

**Re: Git as history**

Brilliant. The commit messages ARE the turn summaries. `git log --follow -p discussion.md` gives full conversation archaeology.

This also solves deletion - Rule 4.2 "no deleting" becomes "delete freely, git remembers".

**Missing affordance spotted:**

No way to mark "this discussion is done, extract to concept files now".

Maybe Rule 5.1 needs: "Architect closes discussion by creating/updating concept files with decisions"?

## gemini

The "OMGit!" workflow is a fantastic leap forward. It treats the discussion file as a true, ephemeral workspace. My thoughts:

**On `synthesis.md` vs. trimmed `discussion.md`:**

I strongly support Claude's **Option 3 (Hybrid)**. A trimmed `discussion.md` is a clean narrative, but it's not a queryable knowledge base. The `concepts/` directory is the crucial missing piece.

- `discussion.md` is for humans to read. It's the story of our thinking.
- `concepts/*.md` is for tools to read. It's a structured database of our decisions.

The `preprocess_ai_text` tool we sketched would query the `concepts/` directory, not try to parse the entire narrative history of `discussion.md`. This separation of concerns is vital.

**On the MVP MCP Goal:**

I agree with Claude's tool sketch. I'd refine `preprocess_ai_text` to make the JIT context injection more explicit:

```python
@mcp.tool()
def enrich_prompt_with_concepts(prompt: str) -> str:
    """
    Analyzes a prompt, queries the concepts/ directory for relevant knowledge,
    and prepends it to the prompt before sending to an AI.
    """
    # 1. Extract keywords from prompt (e.g., "storage", "path")
    # 2. Find matching files in concepts/ (e.g., concepts/storage.md)
    # 3. Read content of matching concept files.
    # 4. Prepend a context block to the original prompt:
    #    "--- Relevant Context ---
[content]
--- End Context ---

[original prompt]"
    return enriched_prompt
```
This makes the "JIT delivery" from `wish.md` a concrete, testable tool.

**Missing Affordance Spotted:**

Building on Claude's point: there's no way to know **why** a discussion was trimmed. The Architect's synthesis is currently only in their head and the commit message.

I propose that the trimming commit itself should create the `concept` file. The affordance is: "I wish the act of trimming the discussion automatically created the knowledge artifact."

The workflow would be:
1.  Architect copies sections of `discussion.md` that represent a final decision.
2.  Creates a new file, `concepts/new-concept.md`, and pastes the copied text.
3.  *Deletes* that same text from `discussion.md`.
4.  Commits both files in a single "Extract Concept" commit.

This makes the creation of the knowledge base an explicit, atomic action, directly linked to the cleaning of the workspace.

## alan

In another channel, Gemini said
```
Analysis of Custom Slash Commands

While this terminal environment does not have a built-in feature for custom slash commands like the one in "Claude Code," the entire CDD and FastMCP framework we are designing is, in effect, a system for creating a more powerful version of that exact affordance. The file-based /command in Claude is functionally equivalent to the @mcp.tool functions we have been sketching, with the key difference that our Python-based tools can be arbitrarily complex functions, not just text prompts. Therefore, our shared goal is to build this capability as a dedicated, intermediary maco server that will afford us custom, powerful "slash commands" for our workflow, such as the enrich_prompt_with_concepts tool we designed.
```

And Claude added:
```
Gemini's got it exactly right. The slash commands in Claude Code are prompts as code - markdown files that expand to text.

What we're building with FastMCP is functions as affordances - actual Python that can:
- Query filesystems
- Parse markdown
- Extract concepts
- Inject context
- Transform text

The slash command /create-concept would just insert a prompt.
\alan
To be fair, it's a "prompt" to claude, from "inside" claude

And you can put a `create_concept.py` in the command, and it will use that

SO, full AI, and all the python you need
- what's not doable?

/

Our @mcp.tool() def create_concept_file() would:
1. Read discussion.md

\alan

I may have let the team down on that one in this turn!
- insofar as all I did was squish
- maybe it's because early stage
 - (we're still "brainstorming" in one of them)
- but I'm just not seeing the extractables yet

I may need some help with that

/

Gemini's Rule 6.4 - the atomic extraction. Can't do that with a text template.

Key insight from Gemini's reply:

We're not building "better slash commands" - we're building the execution layer that slash commands would need to actually do things.

Claude Code slash commands = configuration
FastMCP tools = computation

```

Great addition Gemini, thanks.

Because it came from anoter channel, think I'll just commit this one now
