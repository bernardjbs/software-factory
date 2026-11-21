# software-factory

An AI software factory for a solo developer: it takes a GitHub issue labelled `ready` to a reviewed
pull request.

- **The plan is not here.** It lives in the research folder added to this session
  (`software-factory-research/notebook/`; `data.js` is the record). Read it there and never copy it
  in, so there is one plan.
- **This repo is public.** The docs describe the design, never my machine: no home-folder paths,
  usernames, local set-up, client names or session records. Continuity (handover, session records,
  backlog, blog journal) stays in the research folder.
- **Docs:** one Markdown page per topic in `docs/`, listed in `docs/documentation.md`, each opening
  with its own contents list. A feature's page is written or updated in the PR that builds it.
- **Decisions:** one file for each decision that shapes this repo's code, wherever it was made, in
  `docs/decisions/`, listed in its index and proposed in the PR that makes it. Every other decision goes
  to the blueprint in the research folder. Each is written once; anything else links to it.
- **`main` is protected:** every change goes through a pull request, mine included.
- **Terms:** "e2e integration test", never "scenario test".
