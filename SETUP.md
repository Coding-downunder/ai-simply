# Setup: 5 free skills for Claude Code

You are Claude Code. The user pasted a prompt asking you to follow this file. Install the skills below for them, step by step, and keep your messages short and plain.

## What gets installed

| Skill | What it does | Author | Licence |
|---|---|---|---|
| handoff | Packs a long chat into a note a fresh chat can pick up | Matt Pocock | MIT |
| grill-me (+ grilling, which it uses) | Grills the user on a plan before anything gets built | Matt Pocock | MIT |
| humanizer | Rewrites text that sounds like AI wrote it | Siqi Chen | MIT |
| unlazy | Writes its checks first and proves each one before saying "done" | Leon Lin | MIT |
| teach | A tutor that keeps track of what the user has learned | Matt Pocock | MIT |

Nothing here installs hooks, changes settings, or runs code at install time. It only copies skill folders.

## Steps

1. **Tell the user** in two lines what you're about to install (the table above) and that it copies folders into their Claude skills folder. If the user already named specific skills in their prompt, install only those (always include `grilling` with `grill-me`).

2. **Find the skills folder:** `~/.claude/skills/` (on Windows `%USERPROFILE%\.claude\skills\`). Create it if it doesn't exist.

3. **Check for clashes.** If a folder with the same name already exists there, don't overwrite it. List the clashes and ask the user whether to replace or skip each one.

4. **Download** this repo to a temporary folder:
   `git clone --depth 1 https://github.com/Coding-downunder/ai-simply.git`
   If `git` isn't available, download `https://github.com/Coding-downunder/ai-simply/archive/refs/heads/main.zip` and unzip it instead.

5. **Copy** each chosen folder from `skills/` in the download into the skills folder. Copy the whole folder, including its `LICENSE`.

6. **Delete** the temporary download.

7. **Check it worked:** confirm each installed folder has a `SKILL.md`. Report any that don't.

8. **Finish** by telling the user:
   - which skills are installed
   - to start a new Claude Code session so the skills load
   - how to use each, one line each:
     - `/handoff` when a chat gets long, then paste the note into a new chat
     - `/grill-me` then describe a plan
     - `/humanizer` then paste the text
     - `/unlazy` before a big multi-step task
     - `/teach` then say what you want to learn

## Optional extra for unlazy

unlazy has an optional Stop hook that blocks "done" until every check passes. Do **not** install it as part of this setup. If the user asks for it, point them to `skills/unlazy/README.md` and `skills/unlazy/SECURITY.md` and let them decide.
