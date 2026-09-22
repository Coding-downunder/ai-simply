# Parallel agent sessions: four builds on one codebase at once

On the member data platform I ran four AI coding sessions in parallel, each on its own
project, for about six weeks. This is the working model that let them share one
repository and one database without stepping on each other.

## The working model

- **One branch and one git worktree per session.** A session never edits another
  session's files, because it cannot see them.
- **Merge as soon as a piece works**, not when the project is done. Four branches
  drifting for six weeks is a worse problem than the one branches solve.
- **Flag cross-project impacts, don't fix them.** If session A notices session B's
  view needs a change, it writes it down. It does not edit B's work.
- **An append-only decision log.** Decisions are added, never edited. A reversal is a
  new entry that points at the old one. Six weeks later you can read why a thing is
  the way it is, including the wrong turns.
- **A symptom-to-owner index.** When something breaks across six connected systems,
  the first question is "whose is this". A table answers it.

## The rule that failed, and what replaced it

Database migrations are numbered. The rule was "check the highest number on `main`
and take the next one".

It failed on 2026-08-12. Two sessions both wrote migration `029`, and both had followed
the rule correctly, because `main` was at `025` and neither number had ever been near
it. A number claimed by a sibling branch is invisible from `main` by definition, and
four branches were running.

The replacement is a small script, `next_migration.py`. It checks every local branch,
every remote branch, the working tree and the applied-migrations table, and exits
non-zero if a number is claimed twice. It renames nothing: if one of the two is already
applied, that one keeps the number and the decision is a person's.

A rule that people follow correctly and still collide is not a rule. It is a tool
waiting to be written.

## A corollary, learned twice

A project that replaces a shared database view has to rebase its definition
immediately before applying, not when it was written. Four projects edited one view
in a row. Whoever replaces it wholesale, wins, and silently drops the other three
projects' changes. So: re-read, then replace.

## What this cost and what it bought

The overhead is real: worktrees, a migration checker, a decision log, merge discipline.
The payoff was four projects landing on one live platform in the same six weeks, from
one person directing agents, with no lost work.
