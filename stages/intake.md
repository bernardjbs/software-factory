# Intake

- [Does](#does)
- [Produces](#produces)
- [Gate](#gate)
- [Run log](#run-log)

## Does

- Take only issues the developer wrote or labelled `ready`. Any other issue: stop and say why.
- Answer one of:
  - **go**;
  - **needs info**: ask the author what is missing;
  - **reject**: say why;
  - **too big**: propose a split into smaller issues.
- Guess the size: small, medium or large.
- Suggest a lane:
  - **High risk** if it touches login, money, personal data or deleting data;
  - **Small** if it is clear what done is;
  - otherwise **Ambiguous**.
- A High risk issue is marked High risk and not taken: it is done in the developer's own session, so
  the run ends here.

## Produces

`intake.md` in the run folder (its path is given to you): the issue number and title, the answer
(go, needs info, reject or too big) with its reason, the size, the suggested lane with its reason,
and the lane the developer confirmed.

## Gate

Stop and show the developer the answer, the size and the suggested lane. The developer confirms the lane,
or changes it. Write the confirmed lane to `intake.md`. Only a "go" with a lane other than High
risk goes on to Plan.

## Run log

Only if the project's `CLAUDE.md` names a run-log command (`runlog` below stands for it):

- At the start: `runlog <issue> intake start`
- At the gate, with the developer's verdict and reason:
  `runlog <issue> intake end --verdict accepted|rejected --reason "..."`, and on acceptance
  `runlog <issue> intake end --verdict accepted --lane small|ambiguous|high-risk --size small|medium|large`
