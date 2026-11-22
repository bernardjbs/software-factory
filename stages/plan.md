# Plan

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `intake.md` from the run folder (its path is given to you). Then write a plan holding:

- The approach, which files it touches, and which existing code it reuses (found by searching first).
- The tests:
  - first, the tests that already cover each file being changed (found by what imports it);
  - then each test to write, marked "extend `<existing file>`" or "new, because nothing covers this";
  - each test names the breakage that must make it fail;
  - two tests naming the same breakage means one goes;
  - a refactor needs no new tests: the existing ones should pass unchanged, and if they cannot, the
    plan says the behaviour changes.
- How the work will be proved on the real path, read back from the backend. Where there is no backend
  (a docs or skill change), name how it will be used the way its reader or user would.

## Produces

`plan.md` in the run folder: the plan above, and the developer's verdict with its reason. Plans can
hold detail that must not go public, so it stays in the run folder, never in the repo.

## Gate

Stop and show the developer the plan. The developer approves the plan, or sends it back with why;
sent back, revise it and stop again.

Which plans the developer must approve depends on the lane in `intake.md`:

- **Small:** follows the ladder. The developer approves its plans while Plan is at level 2, then
  samples them.
- **Ambiguous:** the developer approves every plan, whatever Plan's level.
- **High risk:** never reaches Plan; Intake marked it and the factory does not take it.

During the hand runs every plan is approved, so the lane is recorded and changes nothing yet.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> plan start`
- At the gate, with the developer's verdict and reason:
  `runlog <issue> plan end --verdict accepted|rejected --reason "..."`
