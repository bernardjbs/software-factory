# Decisions

- [What goes here](#what-goes-here)
- [Writing a decision](#writing-a-decision)
- [Replacing a decision](#replacing-a-decision)
- [Index](#index)

## What goes here

One short Markdown file for each decision that shapes this repo's code, wherever it was made, added in
the pull request that makes it. Decisions about the plan itself live in the blueprint, outside this
repo. The issue says what was wanted, the pull request says what changed, and the decision file says
what was decided and why it still holds.

A run never decides for me. It proposes a decision in its pull request, with status `proposed`,
flagged at the top of the pull request. Merging the pull request accepts it.

## Writing a decision

Name the file with the next number and a short slug: `0001-run-log-storage.md`. Start it with this
header, then three short sections:

```markdown
# 0001 · Run log storage

- Status: proposed | accepted | replaced by [0009](0009-....md)
- Area: Runtime
- Issue: https://github.com/bernardjbs/software-factory/issues/12
- Pull request: https://github.com/bernardjbs/software-factory/pull/14
- Replaces: [0004](0004-....md) (only if it does)

## Context
What forced a choice, and what was on the table.

## Decision
What was chosen.

## Consequences
What this makes easier, and what it makes harder.
```

Write issue and pull request links in full. GitHub links `#12` in issues, pull requests and
comments, but not inside a file in the repo.

Add a line for it to the [index](#index), and link the decision from the docs page of the feature
it is about.

## Replacing a decision

Before proposing a decision, read the index for lines in the same area, and open any that look
related. If the new decision replaces one:

- the new file says `Replaces:` with a link to the old one;
- the old file's status becomes `replaced by` with a link to the new one;
- both index lines are updated.

The old file is never deleted, so the history stays readable.

## Index

Areas: Workflow, Quality, Runtime, Security, Goals. One folder, no subfolders: each file carries its
area, and the index is grouped by it. Add an area when a decision fits none; a decision spanning two
carries both.

| # | Decision | Area | Status |
|---|---|---|---|
