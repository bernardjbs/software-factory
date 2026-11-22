# Protected files

- [The list](#the-list)
- [How they change](#how-they-change)

## The list

| Path | Why |
|---|---|
| `.github/workflows/` | CI workflows: they run the checks every pull request must pass. |
| `.claude/settings` files | They set what the runner may do. |
| `.claude/hooks/` | The hooks enforce the rules a runner could otherwise skip. |
| `CLAUDE.md` | It tells every runner how the project works. |
| The factory's checks | They decide what counts as passing. |
| The push script | It gates what leaves the machine. |
| The install allow list | It limits which packages a run may add. |
| `stages/` | The stage files are the runner's instructions. |
| `.claude/skills/factory-cycle/` | The skill that runs the stages in order and stops at each gate. |
| `.claude/agents/independent-reviewer.md` | The reviewer that must not be able to edit what it judges. |

## How they change

Only through a reviewed pull request. The push script will enforce this; until it exists, a pull
request that changes one names it under Flags in `stages/pr-template.md`, with the reason and
impact.
