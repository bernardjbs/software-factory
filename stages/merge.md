# Merge

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `review.md` from the run folder (its path is given to you), then:

- Wait: the developer merges. Never automatic; never merge it yourself.
- Then wrap-up and the next-session note, in a hand run only, through the project's own wrap-up.
- An unattended run never writes memory or the handover: it writes only its run note.

## Produces

In an unattended run, the run note in the run folder: the issue, the pull request, whether it merged,
and anything left open. Nothing else. In a hand run, what the project's own wrap-up writes.

## Gate

The developer merges, or does not. Never automatic.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> merge start`
- At the gate, with the developer's verdict and reason:
  `runlog <issue> merge end --verdict accepted|rejected --reason "..."`
