# Check

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `plan.md`, `build.md` (for the branch) and `rounds.md` (absent on the first pass: no rounds
yet) from the run folder (its path is given to you) and check the branch:

- The full test suite, not only the new tests.
- The real path, with the result read back from the backend, not the screen. Where there is no
  backend (a docs or skill change), the real path is using it the way its reader or user would; the
  plan names how.
- Each new test broken on purpose to prove it can fail, then restored. Confirm the break landed and
  the restore landed.
- Types and lint.

A failed check goes back to Build as a fix round: append one line to `rounds.md` in the run folder
(round number, `check`, the reason). Failed checks and change requests share one
cap of 3 fix rounds; before sending a fourth round back, stop and come to the developer with
`rounds.md`.

## Produces

`check.md` in the run folder: each check, the command run, and its result (exit code, counts), the
real-path evidence read back, and for each new test the break made and the failure it gave.

## Gate

None, except the cap: before sending a fourth fix round back, stop and come to the developer with
`rounds.md`.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> check start`
- At the end: `runlog <issue> check end --verdict accepted|rejected --reason "..."`: `accepted` means
  every check passed, `rejected` that it stopped or sent a fix round back.
- For every fix round it sends back: `runlog <issue> check round <n> --reason "..."`
