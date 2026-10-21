---
name: build
description: "Turn the chosen direction into a working prototype inside the host repo: handoff to WORK.md, one task at a time with tests, and verification against the track's criteria. Use it after the direction is chosen, for the next task, or before a checkpoint, freeze or demo."
---

# Build
Arguments: $ARGUMENTS (handoff, next or verify)
Reply in the user's language. Read BRIEF.md and WORK.md if it exists.

## handoff
If the choice is not recorded, ask only which proposal is the base and what to import from the others.
If the brief links a "Final direction" board, read it and its comments: it is the visual specification.
Inspect the host repo: commands, UI, auth, roles, tenancy, persistence, forms, document store, real providers.
The brief's "Stack and patterns" is a constraint: every task uses that stack and follows those patterns, so code
written by different people fits together. A deviation is a decision recorded in WORK.md. With an empty repo, the
first task scaffolds that stack; there are no host components to protect yet, so shadcn `init` is fine there.
Create WORK.md with: problem and scenario, direction, stack and patterns (one line, from the brief), non-goals, input/output contracts, integrations, authorization
boundaries, vertical tasks with one owner each (split a task that spans two owners), files per owner, acceptance
criteria taken from the track, status and evidence. Mark assumptions and blockers. Never assume host APIs that do not
exist: endpoints the track needs are new contracts, written in WORK.md and frozen at the contract freeze. Adapt the direction to the host, do not paste a parallel app.
Porting the board into the app with host components is the designer's task, accepted when the page matches the board.
Where the board and the host design system differ, keep the host components and carry the board's look in tokens scoped
to the new page; changing the global theme needs the team's OK. Record the choice.
Plan how to switch user and role for tests and demo (the host's demo login, or browser profiles): nobody bypasses
protections or writes cookies by hand. Commit WORK.md: it is the shared reference.

## next
Run the next ready task you own in WORK.md. Read the code and tests, add a positive and a negative check, make the
smallest change through existing adapters and components, following the brief's stack and patterns (with shadcn: `add`
only after `--dry-run` and `--diff`, never `init`, `apply` or a preset change on existing components without the team's
OK; the scaffold task of a new repo is the exception), run real commands, update your rows in WORK.md with evidence and limits.
A task that touches a frozen contract: stop and record the decision first. When the task is verified, commit code and
WORK.md together, so the rest of the team starts from the real state.

## verify
Check only this track. Build the checklist from the acceptance criteria, scoring and penalties in the brief, then add:
end to end on the real server; authorization and isolation between users, roles or tenants when the track has them;
error and empty states; the host test runner; caches, exports and public artifacts; no secrets in pages or logs;
no invented numbers in UI or narration. Use the browser when available, never instead of tests.
UI: compare the integrated page with the chosen board and run impeccable's audit if it is installed. Do not fix other
people's files: add each problem to the task list in WORK.md, with its owner, so `next` picks it up.
Classify each requirement as verified, failed, not verified or not applicable, with evidence. Commit WORK.md.
