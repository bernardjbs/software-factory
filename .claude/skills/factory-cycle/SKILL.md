---
name: factory-cycle
description: Run one GitHub issue through the factory's six-stage cycle by hand, in this session, stopping at every gate for the developer. Reads the stage files in `stages/` in order and follows them; adds no stage rules of its own. Use when the developer says "/factory-cycle <issue>", "run issue <n> through the cycle", "hand run issue <n>" or "take issue <n> to a PR".
user-invocable: true
---

# factory-cycle

Take one issue from Intake to Merge by following the stage files, stopping at every gate.

## Usage

```
/factory-cycle <issue number>
/factory-cycle --help
```

If `--help` appears anywhere in the user's invocation, read and display [help.md](help.md) and stop.

## What it does

1. **Set the run folder.** The repo root is `git rev-parse --show-toplevel`. If `FACTORY_RUN_DIR`
   is unset, ask the developer for a folder. Reuse an existing `$FACTORY_RUN_DIR/<issue>-*/`;
   otherwise make `$FACTORY_RUN_DIR/<issue>-<slug>/`, the slug from the issue title. Resolve the
   folder's real path and refuse it if it is the repo root or inside the repo: stage outputs can
   hold detail that must not go public. If the folder already holds stage outputs, say which and
   ask where to resume.
2. **Pin the stage files.** If the run folder holds `stages-commit`, use the commit in it.
   Otherwise run `git fetch origin main` (if it fails, stop and say so) and write
   `git rev-parse origin/main` to `stages-commit` in the run folder. Read every file under `stages/`
   from that commit, including the ones a stage names (such as `stages/protected-files.md`):
   `git show <commit>:stages/<file>`, never the working tree, the run's branch or a later fetch.
   If that commit has no `stages/`, stop and say so.
3. **Run the stages in this order**, reading each in full when it starts and following it as
   written:
   - `stages/intake.md`
   - `stages/plan.md`
   - `stages/build.md`
   - `stages/check.md`
   - `stages/review.md`
   - `stages/merge.md`

   Give each stage the issue number and the run folder's path. If a stage has no `## Gate` or no
   `## Run log` section, stop and say so. When a stage sends work back, go where it says.
4. **Stop at each stage's `## Gate`** until the developer decides; write the decision and its
   reason where the stage says.
5. **Follow each stage's `## Run log`.** If the project's `CLAUDE.md` names no run-log command, say
   so once at the start and go on.

## Gates

- The developer decides at the stages' own `## Gate` sections; this skill skips none. Its only own
  stops are the ones in What it does and below.
- Refuse a run folder inside the repo.
- Never edit `stages/`, this skill, or a file listed in `stages/protected-files.md`, except as
  `stages/build.md` allows. A stage file that is wrong is a new issue: say what is wrong, and stop
  now.

## Operating principles

- The stage files are the recipe; this skill only runs them. Never restate or reword a stage rule
  here, so there is one copy.
- Later, the glue runs the same stage files without this skill and repeats steps 1 and 2 itself;
  every other rule a run needs belongs in the stage files, not here.
