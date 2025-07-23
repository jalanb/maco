# Maco Hub Orchestration Requirements

## Planning Mode: On

The maco project needs to build tooling to orchestrate the hub system defined in the foundational architecture discussion.

## Core Requirements from Architecture

#### The 14-step algorithm needs automation:
1. Channel creation (`mkd channel`)
2. Library file linking
3. Participant invitation and file creation
4. Round coordination (steps 8-13)
5. UPPER.md archival to database
6. Iteration until convergence (empty files)
7. Final HUB.md narrative generation

## Technical Challenges

#### File watching and coordination:
- Detect when all participants have written their files
- Archive UPPER.md files between rounds
- Signal when rounds are complete

#### Multi-AI orchestration:
- Invite AIs in team order
- Coordinate simultaneous file reading/writing
- Handle timing and synchronization
- Build on existing maco chat/UI foundations

#### UI/UX considerations:
- Terminal-first workflow (jalanb requirement)
- Integration with existing iTerm setup
- Real-time status visibility

## Questions

__Gold - Need clarification:__
1. How does maco detect "team order" for AI invitations?
2. What database should store the archived UPPER.md rounds?
3. How do we handle AIs that fail to respond or error out?

__Silver - Implementation details:__
4. File watching vs polling for round completion?
5. Should the final HUB.md be markdown or structured data?

## Immediate Tasks

1. __File system watcher__ - Monitor hub directories for completion
2. __Round coordinator__ - Implement the archive/iterate cycle
3. __AI invitation system__ - Programmatic way to invite AIs to hubs
4. __Narrative generator__ - Combine rounds into coherent HUB.md

This is foundational infrastructure that enables all other hub conversations.

## Citations

- `/Users/jab/jalanb/jalanb/hub/hub/ALAN.md` - Foundational hub architecture and 14-step algorithm (lines 69-87)
- `/Users/jab/jalanb/jalanb/hub/hub/ALAN.md` - Lines 42, 105: maco project ownership
- `/Users/jab/jalanb/macos/maco/CLAUDE.md` - Existing maco project context