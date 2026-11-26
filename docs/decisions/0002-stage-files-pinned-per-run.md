# 0002 · Stage files pinned per run

- Status: proposed
- Area: Security
- Issue: none: built from the factory-cycle design
- Pull request: (added once the pull request exists)

## Context
The stage files are a run's instructions. A run that read them from its own branch, the working
tree or a moving ref could change the rules it is following, mid-run or on resume, without the
developer seeing it.

## Decision
At the start of a run, after the run folder is set (see [0001](0001-hand-run-folder.md)), fetch
`origin/main` once, check it has `stages/`, and write its commit to `stages-commit` in the run
folder. Every file under `stages/` is read from that commit (`git show <commit>:stages/<file>`),
and a resume reuses it. A failed fetch stops the run. The developer re-pins by deleting
`stages-commit`.

## Consequences
A run cannot weaken its own rules: an edit to a stage file on its branch or in the working tree is
never read. A stage file fixed on `main` reaches a running issue only when the developer re-pins.
