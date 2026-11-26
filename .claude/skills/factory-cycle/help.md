# factory-cycle

Runs one GitHub issue through the factory's cycle by hand: Intake, Plan, Build, Check, Review,
Merge. Each stage is a file in `stages/`, read from `origin/main`; the skill follows them in order
and stops wherever a stage's `## Gate` says.

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

Each stage file's `## Gate` section says what you decide there and when the run waits for you.

## Where things land

- Stage outputs: `$FACTORY_RUN_DIR/<issue>-<slug>/`.
- Code: a branch and a pull request, as the stage files say.
