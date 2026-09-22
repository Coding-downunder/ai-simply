# Writing a skill that actually fires

A skill is a folder with a `SKILL.md` that teaches an agent how to do one job. The
common failure is not a bad skill. It is a good skill that never triggers, so the
person concludes "AI doesn't work here" and stops trying.

## The description field is the trigger

The agent decides whether to load a skill from the `description` in its frontmatter,
before it reads anything else. So the description gets the scrutiny, not the body.

Weak:

```yaml
description: Helps with meeting notes.
```

Strong:

```yaml
description: Use when the user pastes a call transcript or rough notes, says
  "write up the meeting", "who agreed to what", "send me a recap", or asks for
  actions and owners from a call, even if they never say the word "notes".
```

The strong version lists the phrases a colleague would actually type. The weak one
describes a topic and hopes.

## Every skill ships with a "Tested with" section

The `SKILL.md` ends with the real prompts it was tested against:

```markdown
## Tested with

- "here's the transcript from this morning, can you write it up" (pasted text)
- "what did we actually decide on pricing yesterday"
- "recap the client call for the team"
```

If a colleague types one of those and the skill doesn't fire, that is a bug with a
reproduction, not a vague complaint.

## Keep the body lean

- Context over constraints. Tell the agent what the job is and what good looks like.
  A wall of "do not" lines gets skimmed and half-followed.
- One job per skill. A skill that does five things fires for none of them reliably.
- Reference files for the long material (formats, examples, checklists). The agent
  loads them when it needs them, so the description and the first screen stay short.

## Read a skill before you install it

A skill is instructions your agent will follow with every permission you have given
it. Before installing one from anywhere, including this repo, read the `SKILL.md`,
check what scripts it runs, what it fetches from the network, and whether it installs
hooks. Then decide.
