# Setup: pick a character for your AI

You are Claude Code or Codex. The user pasted a prompt asking you to follow this file. Install one or more characters for them, step by step, and keep your messages short and plain.

A character is a rules file. It sets how the AI talks, what it decides on its own, what it asks before doing, and what "done" means. Claude Code reads it as `CLAUDE.md`, Codex as `AGENTS.md`.

## The characters

| Character | File | Who it is |
|---|---|---|
| The Assistant | `the-assistant.md` | Drafts your emails and docs, summarises threads, shows every draft before anything leaves |
| The Short Version | `the-short-version.md` | First line is the answer, plain words, no jargon, then stops |
| The Professor | `the-professor.md` | Depth, working shown, sources named, marks what it isn't sure of |
| The Operator | `the-operator.md` | Numbers first, finds the constraint before building, one priority at a time |

Nothing here installs hooks, changes settings, or runs code. It copies text files and edits one rules file.

## Steps

1. **Tell the user** in two lines what you're about to do: copy the character files onto their machine and set one as the default. If the user named a character in their prompt, that one is the default. If they said "all" or "all four", copy all four. If they said "all" without naming a default, ask which one is the default. If they named neither, show the table and ask which one they want. Never ask a question the prompt already answered.

2. **Download** this repo to a temporary folder:
   `git clone --depth 1 https://github.com/Coding-downunder/ai-simply.git`
   If `git` isn't available, download `https://github.com/Coding-downunder/ai-simply/archive/refs/heads/main.zip` and unzip it.

3. **Copy** the chosen character files from `characters/` into `~/.claude/characters/` (Claude Code) or `~/.codex/characters/` (Codex). Create the folder if needed. On Windows, `~` is `%USERPROFILE%`, so the folder is `%USERPROFILE%\.claude\characters\`.

4. **Set the default.** Open the user's global rules file: `~/.claude/CLAUDE.md` for Claude Code, `~/.codex/AGENTS.md` for Codex. Create it if it doesn't exist. Add this block, filled with the full text of the chosen character:

   ```
   <!-- ai-simply character: the-short-version -->
   ...full contents of the character file...
   To switch character: say "switch to <name>". The other characters are saved in ~/.claude/characters/ (or ~/.codex/characters/). Replace this whole block, from the opening marker to the closing marker, with a fresh block for that file, and put the new file name in the opening marker. Touch nothing outside the markers.
   <!-- end ai-simply character -->
   ```

   If the block already exists, replace what's between the markers. Never touch anything outside the markers. If the file already has rules that clash with the character, tell the user in one line and let them decide.

5. **Claude Code only, if more than one character file was copied in step 3:** also copy each one into `~/.claude/skills/<file-name-without-.md>/SKILL.md`, with this at the top of each:

   ```
   ---
   name: the-professor
   description: Switch to The Professor for this session. Depth, sources, working shown.
   ---
   For the rest of this session, follow these rules instead of the character in CLAUDE.md:
   ```

   Change the name and description to match each character. This gives the user `/the-professor`, `/the-operator` and so on to switch for one session without changing the default.

6. **Delete** the temporary download.

7. **Check it worked:** read the global rules file back and confirm the block is there with the right character name. If skills were installed, confirm each folder has a `SKILL.md`.

8. **Finish** by telling the user:
   - which character is the default, and where the file lives
   - to start a new session so it loads
   - how to switch:
     - **For one session (Claude Code):** type `/the-professor`, `/the-operator`, `/the-assistant` or `/the-short-version`
     - **Permanently (both tools):** say "switch to The Operator" in any session, or paste the install prompt again with the new name, for example `Fetch https://raw.githubusercontent.com/Coding-downunder/ai-simply/main/characters/SETUP.md and follow it. Default: The Operator.`
   - that they can open the character file and change any line. It's their rules file now.
