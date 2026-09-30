# Characters: four rules files, pick the one that sounds like you

A rules file is the one thing your AI reads at the start of every session. Claude Code
calls it `CLAUDE.md`, Codex calls it `AGENTS.md`. Without one, every chat starts from
zero and you repeat yourself.

Each character here fills the same four sections differently: how it talks to you,
what it decides on its own, what it asks before doing, and what "done" means.

| Character | Who it is | Best for |
|---|---|---|
| [The Assistant](the-assistant.md) | Drafts your emails and docs, summarises threads, shows every draft before anything leaves | Anyone who writes all day |
| [The Short Version](the-short-version.md) | First line is the answer, plain words, no jargon, then stops | People sick of scrolling |
| [The Professor](the-professor.md) | Depth, working shown, sources named, marks what it isn't sure of | Learning something properly |
| [The Operator](the-operator.md) | Numbers first, finds the constraint before building, one priority at a time | Running a business |

## Install (30 seconds)

Paste this into a new Claude Code or Codex session:

```
Fetch https://raw.githubusercontent.com/Coding-downunder/ai-simply/main/characters/SETUP.md and follow it. Default: The Short Version.
```

Change the name at the end to the one you want, or say `Install all four` and pick a
default when it asks.

## Switching

- **For one session** (Claude Code, when all four are installed): type `/the-professor`,
  `/the-operator`, `/the-assistant` or `/the-short-version`.
- **Permanently**: paste the install prompt again with a different name. It swaps the
  block in your rules file and leaves everything else alone.

## Make it yours

Open the file and change any line. Every character is under 60 lines on purpose. The
Operator's "before any new task" questions come from Alex Hormozi's public business
diagnosis material, rewritten as instructions.

Every file here is MIT licensed. Take it, cut it, ship it.
