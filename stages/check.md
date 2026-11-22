# Check

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `plan.md` from the run folder (its path is given to you) and check the branch:

- The full test suite, not only the new tests.
- The real path, with the result read back from the backend, not the screen. Where there is no
  backend (a docs or skill change), the real path is using it the way its reader or user would; the
  plan names how.
- Each new test broken on purpose to prove it can fail, then restored. Confirm the break landed and
  the restore landed.
- Types and lint.

A failed check goes back to Build as a fix round.

## Produces

`check.md` in the run folder: each check, the command run, and its result (exit code, counts), the
real-path evidence read back, and for each new test the break made and the failure it gave.

## Gate

None.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> check start`
- At the end: `runlog <issue> check end --verdict accepted|rejected --reason "..."`
- For every fix round it sends back: `runlog <issue> check round <n> --reason "..."`
