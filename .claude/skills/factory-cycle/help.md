# factory-cycle

Runs one GitHub issue through the factory's cycle by hand: Intake, Plan, Build, Check, Review,
Merge. Each stage is a file in `stages/`, read from one `origin/main` commit recorded in the run
folder; the skill follows them in order and stops wherever a stage's `## Gate` says.

## Usage

```
/factory-cycle <issue number>
/factory-cycle --help
```

## Before the first run

Set `FACTORY_RUN_DIR` to a folder outside the repo, where each run's stage outputs go (one
subfolder per issue). In this repo, put it in `.claude/settings.local.json`, which is not
committed:

```json
{ "env": { "FACTORY_RUN_DIR": "/path/outside/the/repo/runs" } }
```

Start a new session after setting it. Unset, the skill asks for a folder at the start of each run.

## What you decide

- Intake: confirm the answer and the suggested lane, or change the lane.
- Plan: approve the plan, or send it back with why.
- Review: yes or no to each push; then review the pull request once it is marked ready.
- Merge: you merge, or not.

The run also stops for you when Build cannot follow the plan and when the fix-round cap is reached.
To pick up a stage file fixed on `main` mid-run, delete `stages-commit` in the run folder.

Each stage file's `## Gate` section is the full rule.

## Where things land

- Stage outputs: `$FACTORY_RUN_DIR/<issue>-<slug>/`.
- Code: a branch and a pull request, as the stage files say.
