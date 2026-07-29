# Issue tracker: Local Markdown

Issues and specs (you may know a spec as a PRD) for this repo live as markdown files in `.scratch/`.

## Conventions

- One feature per directory: `.scratch/<feature-slug>/`
- The spec is `.scratch/<feature-slug>/spec.md`
- Implementation issues are one file per ticket at `.scratch/<feature-slug>/issues/<NN>-<slug>.md`, numbered from `01` — never a single combined tickets file
- Triage state is recorded as a `Status:` line near the top of each issue file (see `triage-labels.md` for the role strings)
- Comments and conversation history append to the bottom of the file under a `## Comments` heading

## When a skill says "publish to the issue tracker"

Create a new file under `.scratch/<feature-slug>/` (creating the directory if needed).

## When a skill says "fetch the relevant ticket"

Read the file at the referenced path. The user will normally pass the path or the issue number directly.

## Wayfinding operations

Used by `/wayfinder` and `/through-line`. The **map** is a file with one **child**
file per ticket.

- **Map**: `.scratch/<effort>/map.md` — the low-resolution Notes, resolved indexes,
  fog, and scope body the active skill defines. For `/through-line`, add `Label:
  through-line:map` and `Status: open|resolved` near the top.
- **Child ticket**: `.scratch/<effort>/issues/NN-<slug>.md`, numbered from `01`,
  with the question in the body. A `Type:` line records
  `decision`/`research`/`prototype`/`grilling`/`task`; a `Status:` line records
  `open`/`claimed`/`blocked`/`resolved`.
- **Blocking**: a `Blocked by: NN, NN` line near the top. Use `blocked` only while
  at least one listed ticket is unresolved.
- **Frontier**: scan `.scratch/<effort>/issues/` for files that are `open`,
  unblocked, and unclaimed; first by number wins.
- **Claim**: add `Assignee: <dev>`, set `Status: claimed`, and save before work.
- **Unclaim**: remove `Assignee` and set `Status: blocked` when an unresolved blocker
  exists, otherwise `Status: open`.
- **Resolve**: append the answer under `## Answer` or `## Resolution`, set
  `Status: resolved`, retain the assignee, then update the map through the active
  skill's recording rules.
