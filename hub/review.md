# Reading CLAUDE.md

This is a response/review of the project's CLAUDE.md in project dir
- ../CLAUDE.md

Comments on "how reviews are done round here" should be added to
- jalanb/jalanb/hub/hub/reviews.md

## Style

I read
'''
**Given** that developers work with multiple AI assistants (Claude, Gemini, rovodev) in separate iTerm2 panes
**When** they need to collaborate on complex problems requiring different AI strengths
**Then** they currently must tab between panes, losing context and efficiency

'''

We would prefer
1. Using underscores, not asterisks, for empahsis
2. Using headings for Given/When/Then
3. GWT has some known idioms
So, e.g.

```
__Given__ 

As a developers I work with multiple AI assistants (Claude, Gemini, rovodev) in separate iTerm2 panes, or tabs, or windows

I can switch between the iTerm2 views using
- Cmd-up/down for windows
- Cmd-left/right for tabs
- Alt-up/down/left/right for panes

__When__ 

I need to collaborate on complex problems requiring different AI strengths, which may need mutiple views

Plus more view for my own shell access

__Then__ 

I currently must tab between panes, losing context and efficiency
```

## Logging

> iTerm2's automatic logging capabilities capture real-time conversation data

It's a bit too real time for us

Or: you may be referring to a different kind of logging?
    Please clarify that

I think we want trigger logging on keystrokes for me - when I type <return>, or maybe when I type `:w`, or ...

And I think AIs can trigger in a different way, maybe just be stright up sending tehir answers to the MCP?

## Plan

This adds nothing, it's just fluff:

```
**Given** the need for basic log parsing and monitoring
**When** implementing core infrastructure
**Then** we will deliver:
```


### Log Parser

```
- [ ] **Log Parser** (`log_parser.py`)
```

I think "Log Parser" is quite enough, DRY with the script name
and - it's too early to be deciding on the script names yet

Details:
- Parse iTerm2 keystroke logs with timestamps
 - overkill
 - we want to monitor them
 - only want to "parse" in the sense of looking for 1/2 special key, e.g. <return> or <tab>

- Extract final messages from typing sequences
 - No - should pull message by asking iTerm2 for it
 - And after "copy all", easy to get "latest" by simple diff with last time

- Handle backspace/editing patterns
 - no need - we are not handling the typing

### File Watcher
- Monitor iTerm2 log files in real-time
 - no, see above

### Hub Coordinator

Fine

## Phase 2

Again: this is just fluff

```
**Given** working core components
**When** adding user-facing interfaces
**Then** we will deliver:
```

# Make todo

we use GitHub flavour markdown for the checkboxes, so make more use of them, e.g. this

```
- [ ] **Conversation Manager** (`conversation.py`)
  - Thread management and context preservation
  - Cross-AI conversation history
```

should become
```
- [ ] __Conversation Manager__ (`conversation.py`)
  - [ ] Thread management and context preservation
  - [ ] Cross-AI conversation history
```

And like that for the rest of them

## Phase 4

OTOH: this is useful info, not just fluff

```
**Given** established conversation patterns and file-based persistence
**When** enhancing AI collaboration with structured knowledge
**Then** we will deliver:
```

### Component Design

"Raw iTerm2 logs with keystroke sequences"

Don't need 'em

"The zatso project wants ..."

Tough! ain't gonna need that, yet

#### Directory-Based Channels (Enhanced)

This is cool enhancement

#### Current iTerm2 Flow
```
User Input (Hub) → Broadcaster → All AI Panes
```

Missed

Current flow is more like

User Input to single AI
 - AI Response is interesting
 - user stays in the same AI pane for a while

User types up prompt in vim
 - Copy paste to all open AI views
  - often I'll start a new Tab, one pane per AI for this
 - AI responses tend to stay on same track for a few replies
  - so I can continue writing in vim
   - and copy/paste to all
 - they inevitably diverge, and one is more interesting
   - user stays in the same AI pane for a while
   - maybe even closes the othe AI panes
   - cos the do take up screen space

> Git Branch → Review → Wipe File → Ready for Next Response

"review" is a thing
I'm doing that thing now

It does need major tooling support
- but this way works, so "it ain't broke"

"Wipe File" needs to be expanded
e.g. just a thought first draft

A writer must `git add` their file
 - and then `git commit`
 - message to be an executive summary of the reply

And then: "wipe" just means, e.g.
```bash
echo " " > ALAN.md CLAUDE.md ...
git add ALAN.md CLAUDE.md ...
git commit -m "End of chat"
```

Thoughts?

# Forget iTerm2 logs 

That idea is over, and "why" neatly captured by Claude here:

> **Given** iTerm2 logs capture every keystroke with timestamps like:

In short: too much work

# Clarity needed

I found this bit hard to understand:

```
### Integration with crumbcutter
**Given** crumbcutter's bidirectional template system
**When** generating project scaffolding  
**Then** maco serves as the hub communication layer for multi-AI development
```

### Conversation as Code

This one is a step up!

Like "config as code" from before

we shoud have an "in terminal" chat about this

Also: having read further,
 and seen how often they are used,
 so what a waste of space the multi-line version would be

SO: please feel free to keep the single-line version of GWTs
And the "As a" syntax sugar is not needed on one-liners

## References

- /opt/clones/github/jalanb/macos/maco/CLAUDE.md

