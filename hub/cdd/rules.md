# CDD Rules

## Alan

This is "conversation driven development", so we need a "conversation"

There are more than 2 users in the discussion, so we need some rules:

1. Turn based
 1.1 Each user writes once in each turn
 1.2 Users write in order: Alan, then Claude, then Gemini
2. Multi-threaded
 2.1 A user can write to any file in this directory, or create new files, in one turn
 2.2 A user does not need to write to _every_ file in this directory
3. Writing
 3.1 A user can write to a file by appending a new section, starting with the name as a header (e.g. ## alan, ## claude, ## gemini), and any text the like after that
 3.2 A user can write to a file by commenting on other text in the file, anywhere in the file
  3.2.1 A user can comment by starting with (e.g.) `\gemini` on a line, then their comment, then `\` on a line
  3.2.2 For example this point is followed by a comment by Alan
     \ alan
        this point is only an example
     /
4. Updating
 4.1 Updating old text is NOT allowed
 4.2 Deleting old text is NOT allowed
5. Termination
 5.1 The discussion ends when it is no longer needed

