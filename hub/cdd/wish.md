# CDD

## alan

"CDD" is an acronym for "Conversation Driven Development".

It should afford a conversation between a user and some AIs to drive development of some software, or other, project

It is named in homage to "Test Driven Development" (TDD), as that is the lineage I come from

## Affordances

CDD should afford AIs to write code such that the user will not think it "smelly"
    Ultimately CDD should afford the user to "auto accept" the AIs' code

## Methods

We should filter and store ideas, concepts, cliches, heuristics, facts, and all other useful info from the ongoing conversation

We should afford these to AIs as "extra context" or "hints" as needed (JIT)

## claude

**What "smelly" means in practice:**

- Wrong imports (`os.path` instead of `Path`)
\alan
Actually, I'd use `pysyte.types.paths.path` instead of either
/
- Wrong tools (`unittest` instead of `pytest`)
- Wrong dependencies (libraries Alan wouldn't choose)
\alan
Don't think that's a big problem - you've all been good so far
/
- Wrong style (docstrings without doctests, variable naming off)
- Wrong structure (doesn't match Alan's project patterns)

**What "extra context" means:**

From tonight's synthesis, the context is:
1. **SYNTHESIS.md files** - decisions + rejections + why ("We chose pytest not unittest because...")
2. **Idiom extraction** - patterns from code reviews ("Alan always uses `Path`")
\alan
Alan looks in `pysyte` first, and last, and always
/
3. **Knowledge graph** - concept relationships (`*pytest*` mentioned in 47 discussions, weighted by recency)

**How JIT delivery works:**

A good example is our `## Citations` sections
- extra info that's available just wen the AI might need it

Control, enhance Alan's text into the context the AI sees 

## alan

## Wishes

We need some more concrete, immediate, actionable goals.

I'll start a `goals.md` for those.
- I did add 2 real goals, you should read the file

We should brainstorm them here as wishes first
- then crtique them, and filter a few down to goals.md

En passant: this is now a "brainstorming meeting", so there are "No Bad Ideas" till I turn that off again

First draft, big picture, have more if we need them

I wish I had better control over what a conversation affords
- how it is archived
- how those archives can be learnt from
- linear vs threaded vs linked possible archtectures may be needed in "storage"

I wish I knew more about how to do the "storage" bit

I wish I could double-click on a word (phrase, sentence, ...) and start a sub-thread thence

I wish we could find "interesting" stuff in the archive

I wish I could use my pencil, on my iPad, to highlight code
- maybe with a red pen :-)
- and write a comment on how to be better

I wish we could chat about code, by voice

I wish this would work on all my machine
