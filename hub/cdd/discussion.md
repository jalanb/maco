# Chat about CDD

CDD is new idea arising from chat 
  It encapsulates many important ideas to afford better chats

CDD is "Context Driven Development"
  In homage to TDD, and relying on it

## Chats

Development with many AIs should be chat-based

Development with me should also be chat-based because, e.g.
- many good ideas are small but mentioned often

## Decisions

We need an _Architect_ to make _Decisions_
- Add a few goals and decide how to reach them
- Notice what decisions user keeps making about "good code"

because those decisions will be what's added to the system
 - to allow further and further automation over time


A decision doesn't exist in a vacuum; it's part of a chain of reasoning.
 - start thinking about _linkability_ now

## Menu

This one is 100% dogfooding

## Citations

- ./goals.md
- ./rules.md
- ./wish.md

## Dependencies

- FastMCP


## claude


Keep this discussion pure dogfooding. No tooling yet. 

Then : build the simplest FastMCP tool that would've helped this discussion (probably `start_round()` and `comment()`).


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

\alan

For now it looks like "the start of discussion.md"

/

**Option 1: Keep discussion.md, trim continuously**
- Pro: Single source of truth, git history preserves full context
- Pro: Natural evolution through editing
- Con: File grows unbounded (even trimmed, it accumulates)
- Con: Hard to query "what did we decide about storage?" without reading whole file

\alan

Good pros

Nothing in the cons that couldn't be addressed by _extracting_ more info

Need ideas about what "extracting info from discussion.md to new files" looks like

/

**Option 2: Extract synthesis.md from discussion.md**
- Pro: Clean decision artifact ("We chose X, rejected Y because Z")
- Pro: Queryable - one file per decision/topic
- Pro: Templates for FastMCP tools to extract
- Con: Duplication - decision exists in both files

\alan

Con: `synthesis.md` can never be a single file

Come back in 5 years it'll be a huge sprawling mass, probly have networks involved :-)

I don't see that our goal can be "a thing"
- except maybe that "a knowledge base" can be "a thing"

So not "a synthesis", more "a synthesising"

Sounds like a decision to me, but open to counter-arguments

/

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

\alan

Me too

That one seems much better to me, no single things
- files, and dirs, and sub-dirs
 - sure you could build a whole hierarchy of knowledge in there!

Sounds like another decision
- unless Gemini has some _good_ reasons :-)

/

discussion.md is the workspace - trim it aggressively
Concept files are the knowledge base - extract when decisions solidify

\alan

yes
/

This matches the `*concept*` pattern from knowledge-graph.md and gives us queryable artifacts without duplicating everything.

\alan

TMM about knowledge-graph.md
/

**Re: Git as history**

Brilliant. The commit messages ARE the turn summaries. `git log --follow -p discussion.md` gives full conversation archaeology.

This also solves deletion - Rule 4.2 "no deleting" becomes "delete freely, git remembers".

\alan

That's a good example for why I prefer "affordance":

`git` affords us deletion

/

**Missing affordance spotted:**

No way to mark "this discussion is done, extract to concept files now".

\alan

I think we can afford that, indeed at two levels:
- when there are no commits to any files in a full turn
- when `discussion.md` is empty

/

Maybe Rule 5.1 needs: "Architect closes discussion by creating/updating concept files with decisions"?

\alan

Or he closes it by extracting every last jot from the discussion into the concepts

And:

This file now has a "nameless section" at the start
- after which we all comment with "## alan`, etc"
- and that leading nameless section id kinda now "the minimal context you need to understand the discussion"
- so we could decide the discussion is over if:
  - all the "named sections" are empty, or missing

/

## gemini

The "OMGit!" workflow is a fantastic leap forward. It treats the discussion file as a true, ephemeral workspace. My thoughts:

**On `synthesis.md` vs. trimmed `discussion.md`:**

I strongly support Claude's **Option 3 (Hybrid)**. A trimmed `discussion.md` is a clean narrative, but it's not a queryable knowledge base. The `concepts/` directory is the crucial missing piece.

\alan

OK, we are all in on that one
- We should add a goal for it
- Claude - the hybrid idea was yours, you should do the honours: please add it to `goals.md`


/

- `discussion.md` is for humans to read. It's the story of our thinking.
\alan

Also for AIs - you guys wake up knowing __nothing__, this is basic context 101
 - you need it
/

- `concepts/*.md` is for tools to read. It's a structured database of our decisions.

The `preprocess_ai_text` tool we sketched would query the `concepts/` directory, not try to parse the entire narrative history of `discussion.md`. This separation of concerns is vital.

\alan

yes

/


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

\alan

I'd just like to interject here to marvel at that comment in `def enrich_prompt_with_concepts()`

Well done Gemini!
- it's a fully formed wee plan for the function
- which might not be the best comment after all the code gets filled in
- but it is the ___perfect___ artifact for us in this chat
 - when we are at the "still planning, not ready for code" stage


And also to commend it further for being a comment, and not in the docstring
- docstring is for the callers
- comment is for the coders.

And also to provide something which should be extracted, not just deleted
- that is an "Alan preference" that should end up applicable accross many projects
- it is also an distinct artifact that we might use in these chats more often

So it looks like it might get extracted from `discussion.md` down into `concepts/` more that one way.

Also notice an implication - we will probably need both
- global knowledge
- project knowledge

/

**Missing Affordance Spotted:**

Building on Claude's point: there's no way to know **why** a discussion was trimmed. The Architect's synthesis is currently only in their head and the commit message.

\alan

Excellent point again

Shall consider below
/

I propose that the trimming commit itself should create the `concept` file. The affordance is: "I wish the act of trimming the discussion automatically created the knowledge artifact."

The workflow would be:
1.  Architect copies sections of `discussion.md` that represent a final decision.
2.  Creates a new file, `concepts/new-concept.md`, and pastes the copied text.
3.  *Deletes* that same text from `discussion.md`.
4.  Commits both files in a single "Extract Concept" commit.

This makes the creation of the knowledge base an explicit, atomic action, directly linked to the cleaning of the workspace.

## alan

> explicit, atomic action

Yes - go all in on git for that.
 - But now I need tooling

Last time I deleted  10...50 lines
- Many were just "now redundant"
- but even then it's too many for doing a "git commit" for each line
- at least if "git commit" means
 1. switch to a different window for shell
 2. type "git commit"
 3. type the message
 4. quit vim
 5. back to original window

we'll need to afford me a better UI


