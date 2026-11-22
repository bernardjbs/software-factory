# Review

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

Read `plan.md`, `build.md` (for the branch and Build's notes), `check.md` and `rounds.md` from the
run folder (its path is given to you), then:

- **Gate:** every push waits for the developer's word, fix-round pushes included (until the push
  script exists). Write the word to `review.md`. On a no to a push, stop for the developer; the pass
  ends `rejected` (see Run log).
- Open a draft pull request whose top follows the fixed layout in `stages/pr-template.md`: flags
  (protected files with reason and impact, changed existing tests with why, new packages), what the
  issue asked and what changed, what was checked, decisions this change makes that the issue did not
  ask for, what the reviewers found and how each was resolved; then the full diff. A file listed in
  `stages/protected-files.md` that the change touches is audited first by the independent reviewer
  and named under Flags, negative impact first.
- Run the reviews on the draft, in this order:
  1. the independent reviewer (`.claude/agents/independent-reviewer.md`; cannot edit what it judges;
     "break it, don't confirm it");
  2. Claude's review (`/code-review`);
  3. a security review (`/security-review`), on every pull request.
- The project reviewer's checklist for production-grade code, once it exists; until then the
  independent reviewer works from the same checklist.
- Failed checks and reviewer change requests share one cap of 3 fix rounds, counted across Build,
  Check and Review. Each round goes back to Build: first write the change request to `review.md`,
  then append one line to `rounds.md` in the run folder (round number, `review`, the reason). Before
  sending a fourth round back, stop and come to the developer with `rounds.md`.
- A decision the change makes is proposed as a file in the decisions folder the project's
  `CLAUDE.md` names, after checking its index for one it replaces.
- The feature's docs page is updated in the same pull request.
- **Gate:** the pull request is marked ready; the developer reviews. A change request from the
  developer then is a fix round, sent back to Build like a reviewer's.

## Produces

`review.md` in the run folder: the issue number, the developer's word on each push, the pull request
link, each reviewer's findings and how each was resolved, each change request sent back, the fix
rounds used, the decisions proposed, and Build's notes from `build.md`. The same findings go in the
pull request's "What the reviewers found".

## Gate

Two stops for the developer:

1. Before every push: the developer's word to push, or no.
2. After the reviews pass: the pull request is marked ready and the developer reviews it.

Also stop before a fourth fix round, with `rounds.md`.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it).
Once per pass:

- When the pass starts: `runlog <issue> review start`
- When it ends: `runlog <issue> review end --verdict accepted|rejected --reason "..."`: `accepted`
  when the pull request is marked ready, `rejected` when it sends a fix round back or stops (the
  cap, or the developer says no to a push). The word on a push goes in `review.md`, not the run log.
- For every fix round it sends back: `runlog <issue> review round <n> --reason "..."`
