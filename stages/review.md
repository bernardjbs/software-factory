# Review

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `plan.md` and `check.md` from the run folder (its path is given to you), then:

- **Gate:** push the branch only on the developer's word (until the push script exists).
- Open a draft pull request whose top follows the fixed layout in `stages/pr-template.md`: flags
  (protected files with reason and impact, changed existing tests with why, new packages), what the
  issue asked and what changed, what was checked, decisions this change makes that the issue did not
  ask for, what the reviewers found and how each was resolved; then the full diff. A file listed in
  `stages/protected-files.md` that the change touches is named under Flags.
- Run the reviews on the draft, in this order:
  1. the independent reviewer (cannot edit what it judges; "break it, don't confirm it");
  2. Claude's review (`/code-review`);
  3. a security review (`/security-review`), on every pull request.
- The project reviewer's checklist for production-grade code, once it exists; until then the
  independent reviewer works from the same checklist.
- Failed checks and reviewer change requests share one cap of 3 fix rounds, counted across Build,
  Check and Review. Each round goes back to Build. Past the cap, stop and come to the developer with
  the log.
- A decision the change makes is proposed as a file in the decisions folder the project's `CLAUDE.md`
  names, after checking its index for one it replaces.
- The feature's docs page is updated in the same pull request.
- **Gate:** the pull request is marked ready; the developer reviews.

## Produces

`review.md` in the run folder: the pull request link, each reviewer's findings and how each was
resolved, the fix rounds used, and the decisions proposed. The same findings go in the pull request's
"What the reviewers found".

## Gate

Two stops for the developer:

1. Before the push: the developer's word to push, or no.
2. After the reviews pass: the pull request is marked ready and the developer reviews it.

Also stop when the 3 fix rounds are used up, with the log.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> review start`
- At each gate, with the developer's verdict and reason:
  `runlog <issue> review end --verdict accepted|rejected --reason "..."`
- For every fix round: `runlog <issue> review round <n> --reason "..."`
