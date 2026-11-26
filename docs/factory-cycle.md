# The factory cycle

- [What it is](#what-it-is)
- [Why](#why)
- [Goals, non-goals, anti-goals](#goals-non-goals-anti-goals)
- [Approaches considered](#approaches-considered)
- [The stages](#the-stages)
- [How the stages hand over](#how-the-stages-hand-over)
- [Lanes](#lanes)
- [Where things live](#where-things-live)
- [The hand-run setting](#the-hand-run-setting)

## What it is

The factory's own development cycle: the steps one issue goes through, from a `ready` issue to a
merged pull request. It is written once, as one Markdown file per stage, and followed by two
runners:

- **A hand run:** a Claude Code session with the developer, using the `factory-cycle` skill. Claude
  does each stage; the developer decides at the gates.
- **The glue, later:** the factory's main program starts Claude headless in a sandbox, once per
  stage, and hands it that stage's file. It is not built yet.

## Why

- **Hand runs must prove the factory's own recipe.** If the hand runs and the glue read two copies
  of the instructions, the copies drift and the run log proves the wrong one.
- **Quality first.** For now the priority is output quality: the process, production-grade code
  and security. Time and throughput are measured in the run log and tuned later.

## Goals, non-goals, anti-goals

**Goals**

- Every issue goes through the same six stages, with the same quality rules.
- One copy of each stage's instructions, read by both runners.
- Each stage's start, end and the developer's verdict can be written to the run log.

**Non-goals (separate pieces of work)**

- The run log itself, the glue and the push script.
- Big multi-task work: that keeps its own flow (spec, plan, subagents), and each task of such a
  plan becomes its own issue that goes through this cycle.

**Anti-goals (a failure even if it works)**

- The builder approving its own work.
- Duplicate tests: a new test file for code that already has one.
- A second copy of the recipe anywhere.
- A run able to change its own stage files without the developer seeing it.

## Approaches considered

For how much process each issue gets:

| Approach | Trade-off | Picked |
|---|---|---|
| A. The full multi-task flow on every issue | Top quality, mostly overhead on a small issue | No |
| **B. Quality-first, sized to the issue** | Keeps what catches defects, drops the rest | **Yes** |
| C. Build, then Claude's review only | Fast, but the builder effectively approves itself | No |

Option B keeps the independent review, tests proven able to fail, whole-suite checks and checks on
the real path. It drops the machinery for splitting work into many delegated tasks.

For where the instructions live:

| Approach | Trade-off | Picked |
|---|---|---|
| **Stage files in this repo, read by both runners** | One copy, tested by hand runs | **Yes** |
| Everything inside a general dev-cycle skill | Less today, but the recipe must move later | No |

## The stages

Each stage file says what the stage does, what it produces, where a gate stops it for the
developer, and what it writes to the run log. The rules live there, not here.

1. [Intake](../stages/intake.md): whether the issue can be taken, its size and a suggested lane.
2. [Plan](../stages/plan.md): the approach, the tests and how the work is proved, for approval.
3. [Build](../stages/build.md): a branch, the tests first, then the code, then a tidy-up pass.
4. [Check](../stages/check.md): the full suite, the real path, new tests proved able to fail.
5. [Review](../stages/review.md): a draft pull request and its reviews, then ready to review.
6. [Merge](../stages/merge.md): the developer merges, then the wrap-up.

Two more files in `stages/` are read by the stages: the
[pull request template](../stages/pr-template.md) and the
[protected-files list](../stages/protected-files.md).

A run reads its stage files from one commit of `main`, pinned when the run starts, so it cannot
change the rules it follows: [decision 0002](decisions/0002-stage-files-pinned-per-run.md).

## How the stages hand over

In a hand run the session carries everything. The glue will start a fresh Claude for each stage, so
each stage writes what it produced to a file in the run's own folder, and the next stage reads it:
`intake.md`, `plan.md`, `build.md`, `check.md`, `rounds.md` (fix rounds), `review.md` and, in an
unattended run, `run-note.md`. The folder also holds `stages-commit`, the pinned commit.

The runner passes the folder's path to each stage. It sits outside the repo, since plans and other
outputs can hold detail that must not go public:
[decision 0001](decisions/0001-hand-run-folder.md). The stage files name these outputs, so both
runners use the same words.

## Lanes

Intake suggests a lane and the developer confirms it. The factory's plan gives each stage a trust
level that rises with its track record; the lane decides how much of that trust an issue gets:

- **Small:** the developer approves its plans until Plan has earned enough trust, then samples
  them.
- **Ambiguous:** the developer approves every plan, whatever Plan's level.
- **High risk:** done in the developer's own session until Check and Review have both earned enough
  trust on that project. Intake marks it and the factory does not take it.

During the hand runs every plan is approved, so the lane is recorded and changes nothing yet.

## Where things live

| What | Where |
|---|---|
| Stage files | [`stages/`](../stages/intake.md), one file per stage, listed above |
| Pull request template | [`stages/pr-template.md`](../stages/pr-template.md) |
| Protected-files list | [`stages/protected-files.md`](../stages/protected-files.md) |
| The hand-run skill | [`.claude/skills/factory-cycle/`](../.claude/skills/factory-cycle/SKILL.md) |
| Independent reviewer | [`independent-reviewer.md`](../.claude/agents/independent-reviewer.md) |
| Decisions this cycle makes | [`docs/decisions/`](decisions/README.md) |
| Each run's stage outputs | The run folder, outside the repo |

The skill is a thin runner: it reads the stage files in order, runs them in the session and stops
at each gate. It holds no stage rules of its own. Runs see only their own clone, so whatever they
need is in the repo. The stage files and the skill are themselves protected files, changed only
through a reviewed pull request.

## The hand-run setting

A hand run needs one setting: `FACTORY_RUN_DIR`, a folder outside the repo where each run's
outputs go, one subfolder per issue. Set it once per machine, in a settings file that is not
committed; if it is unset, the skill asks for a folder at the start of each run. The skill refuses
a folder inside the repo. The [skill's help](../.claude/skills/factory-cycle/help.md) shows how to
set it.
