# Gates and evidence: what "done" means

The most expensive word an agent says is "done". It usually means "I stopped".

So every task with two or more steps opens with a gates ledger, written before any
work starts. Each gate is one observable outcome, the command that checks it, and the
exact output that proves it. The task is finished when every gate has real output
pasted against it. Not a summary of the output. The output.

## The format

```
GATES

1. Parser matches the hand-built tracker
   CHECK:  python compare.py --tracker tracker.csv --parsed out.json
   EXPECT: mismatches: 0 of 404

2. Read-only database role cannot write
   CHECK:  python scripts/prove_readonly.py
   EXPECT: INSERT refused, UPDATE refused, DELETE refused, DDL refused

3. Scheduled job ran in the last hour
   CHECK:  select max(finished_at) from job_runs where job = 'ingest';
   EXPECT: a timestamp less than 60 minutes old
```

Then the work. Then the same ledger again with the real output under each gate.

## Why write it first

- **It turns the task into a test.** "Fix the parser" becomes "402 of 404 must match".
  The agent can't drift, because the finish line is on the page before it starts.
- **It catches the wrong task.** If I can't write a gate, I don't understand the ask yet.
  Better to find that out before an hour of work.
- **It stops the pleasant lie.** An agent that has to paste `mismatches: 0 of 404`
  can't say "the parser now handles all cases".

## Rules I hold to

- Every field a check prints gets compared to an expected value. A check that prints
  a number nobody compares is decoration.
- Verify the thing that routes, not the thing that exists. A config file being present
  proves nothing. The setting being read by the running process does.
- Numbers prove plumbing, eyes prove quality. Anything visual gets rendered and looked at.
- Run the whole test suite and grep for failures. "The tests I touched pass" is not a gate.
- Delegated work carries its gates in the brief. I verify the ledger, never the agent's word.

## Enforcing it

I use [unlazy](https://github.com/Leonxlnx/unlazy) by Leon Lin (MIT). It adds an optional
Stop hook that blocks the "done" message until every gate in the ledger has passing
evidence. If there is no ledger, the hook stays silent and normal chat is unaffected.

I didn't write unlazy. I adopted it because it enforces the thing I was already asking
for, and a hook that can't be talked out of it beats a rule that can.
