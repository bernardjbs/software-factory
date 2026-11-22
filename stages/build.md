# Build

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `plan.md` from the run folder (its path is given to you), then:

- Name the branch `<issue number>-<short-slug>`.
- Write the tests first and show each failing for the breakage the plan names; then the code.
  Keep to one concern only: anything else the work turns up becomes a note for the developer, in
  `build.md`.
- Never edit a file listed in `stages/protected-files.md` unless the issue asks for it; when it does,
  `plan.md` names it and Review flags it.
- No per-change approval: the developer saw the plan and will read the PR.
- End with a tidy-up pass (`/simplify`), so the checks and every reviewer see the code in its final
  shape.
- Run `gitleaks` before each commit; a reported leak stops the commit.

A fix round (a failed check or a reviewer's change request) comes back here. Also read its cause:
`check.md` (a failed check) or `review.md` (a reviewer's change request), and `rounds.md`. Make the
fix, then run the tidy-up again, so it also runs on the fixes. Failed checks and change requests share
one cap of 3 fix rounds, counted in `rounds.md`.

## Produces

Commits on the branch, and `build.md` in the run folder: the branch name, the commits, and the notes
for the developer (what "one concern" set aside). Check and Review read `build.md` for the branch.

## Gate

None by default: the plan was approved. Stop for the developer only if the work cannot follow the plan;
say what differs and why.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> build start`
- At the end: `runlog <issue> build end --verdict accepted|rejected --reason "..."`: `accepted` means
  the stage finished, `rejected` that it stopped.
- For every fix round: `runlog <issue> build round <n> --reason "..."`
