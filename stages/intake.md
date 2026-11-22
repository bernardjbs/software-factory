# Intake

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

- Take only issues the developer wrote or labelled `ready`. Any other issue: stop and say why.
- Answer one of:
  - **go**;
  - **needs info**: ask the author what is missing, in an issue comment;
  - **reject**: say why;
  - **too big**: propose a split into smaller issues.
- Guess the size: small, medium or large.
- Suggest a lane:
  - **High risk** if it touches login, money, personal data or deleting data;
  - **Small** if it is clear what done is;
  - otherwise **Ambiguous**.

## Produces

`intake.md` in the run folder (its path is given to you): the issue number and title, the answer
(go, needs info, reject or too big) with its reason, the size, the suggested lane with its reason,
and the lane the developer confirmed.

## Gate

Stop and show the developer the answer, the size and the suggested lane.
The developer confirms the lane by giving the issue its lane label (`lane: small`,
`lane: ambiguous` or `lane: high risk`), changing it if need be.
Write the confirmed lane to `intake.md`.

If the confirmed lane is High risk, the issue keeps its `lane: high risk` label and the run ends: it
is done in the developer's own session until Check and Review both reach level 3 on that project.
Only a "go" with a lane other than High risk goes on to Plan.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> intake start`
- At the gate, once. `accepted` when the run goes on to Plan (a go in a lane other than High risk,
  whether the developer kept Intake's lane or changed it), with the confirmed lane and Intake's
  size:
  `runlog <issue> intake end --verdict accepted --lane small|ambiguous|high-risk --size small|medium|large`
- `rejected` when the run stops here (needs info, reject, too big, or a High risk lane), with the
  answer in `--reason`: `runlog <issue> intake end --verdict rejected --reason "..."`
