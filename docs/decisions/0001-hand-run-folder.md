# 0001 · Hand-run folder

- Status: proposed
- Area: Security
- Issue: none: built from the factory-cycle design
- Pull request: (added once the pull request exists)

## Context
Each stage of the [factory cycle](../factory-cycle.md) writes its output to a file the next stage
reads. Those outputs, plans especially, can hold detail that must not go public, and this repo is
public. Kept inside the repo, one careless commit would publish them.

## Decision
A run's outputs go in a folder outside the repo, one subfolder per issue. The folder is named by
the `FACTORY_RUN_DIR` setting; when it is unset, the skill asks for one at the start of the run.
The skill resolves the folder's real path and refuses one that is the repo root or inside the repo.

## Consequences
Nothing private can be committed by accident, since it never sits in the working tree. Each machine
sets the variable once, in a settings file that is not committed, or the developer names a folder
on every run.
