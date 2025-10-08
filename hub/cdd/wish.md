# CDD

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
- Wrong tools (`unittest` instead of `pytest`)
- Wrong dependencies (libraries Alan wouldn't choose)
- Wrong style (docstrings without doctests, variable naming off)
- Wrong structure (doesn't match Alan's project patterns)

**What "extra context" means:**

From tonight's synthesis, the context is:
1. **SYNTHESIS.md files** - decisions + rejections + why ("We chose pytest not unittest because...")
2. **Idiom extraction** - patterns from code reviews ("Alan always uses `Path`")
3. **Knowledge graph** - concept relationships (`*pytest*` mentioned in 47 discussions, weighted by recency)

**How JIT delivery works:**

A good example is our `## Citations` sections
- extra info that's available just wen the AI might need it

Control, enhance Alan's text into the context the AI sees 


