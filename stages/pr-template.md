# Pull request template

The fixed layout for the top of every factory-cycle pull request, above the full diff. Review fills
it in; keep every heading, writing "None" where a section is empty.

- [How to write it](#how-to-write-it)
- [Flags](#flags)
- [What the issue asked](#what-the-issue-asked)
- [What changed](#what-changed)
- [What was checked](#what-was-checked)
- [Decisions](#decisions)
- [What the reviewers found](#what-the-reviewers-found)

## How to write it

The developer reads this before the diff, so it must scan in seconds:

- One fact per bullet, plain words first; a path or command only where the reader needs it.
- No line breaks inside a sentence: GitHub shows each one.
- A list of results is a table; each finding is one line, what was wrong, then what changed.
- Commit hashes go last, never mid-sentence.

## Flags

- **Protected files:** each file from `stages/protected-files.md` this change touches and what it
  is, then **Risk:** the negative impact, then **Audited:** who reviewed it.
- **Changed existing tests:** each existing test changed, and why.
- **New packages:** each package added.

## What the issue asked

Closes #<issue>. The issue's ask in a sentence or two.

## What changed

What the change does, file by file where it helps.

## What was checked

The full test suite, the real path (read back from the backend, or used the way its reader or user
would), each new test broken on purpose, types and lint: the command and result for each.

## Decisions

Decisions this change makes that the issue did not ask for, each linked to its file in the decisions
folder.

## What the reviewers found

Each finding from the independent reviewer, `/code-review` and `/security-review`, and how each was
resolved.
