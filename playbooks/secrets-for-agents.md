# Secrets for agents: the value never reaches the transcript

An AI coding agent needs API keys to do real work. The moment a key appears in a chat,
it is in a transcript, probably in a log, and possibly in a commit. So the rule is not
"be careful with keys". The rule is that the agent never sees the value at all.

## The setup

1. Every credential lives in the password manager. Not `.env`, not JSON, not a shell export.
2. A small wrapper script around the password manager's CLI reads a value by name.
   Mine is called `kp`. It can read. It cannot write.
3. Records are titled `<service>--<secret-name>`, for example `stripe--webhook-secret`,
   so an agent can find what it needs by searching the service name.

## How the agent uses it

The value is referenced inline, so it goes straight from the vault into the process
environment and never through the model:

```bash
STRIPE_KEY=$(kp pass stripe--api-key) python sync_customers.py
```

The agent writes that line. It never runs `kp pass stripe--api-key` on its own and
reads the output, because then the value is in the transcript.

## What the agent is told

From my rules file:

- Never print a secret. Reference it inline.
- If the wrapper returns nothing, the session most likely lapsed. A person logs in
  again in a real terminal.
- Never ask for the master password in chat.
- The wrapper cannot write. New records get created by a person in the vault.

## Why the wrapper can't write

An agent that can create credentials can also overwrite them. Keeping writes with a
person costs me thirty seconds now and then. It removes an entire class of incident.
See [structural-guards.md](structural-guards.md).

## Before anything ships

Anything leaving the machine gets scrubbed: no keys, no real names, no phone numbers,
no team first names. That check is a gate, not a habit.
