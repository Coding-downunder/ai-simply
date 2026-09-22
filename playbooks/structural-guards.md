# Structural guards: a guard beats a rule

A written rule is the last line of defense, not the first. An agent under pressure
reasons its way around "don't write to production". It cannot reason its way around
a database login that has no write permission.

So wherever an agent touches something real, I look for the version of the rule that
is enforced by the system, not by the agent's good behavior.

## The pattern

| Written rule | Structural guard |
|---|---|
| "Only read from the database" | A Postgres role granted `select` and nothing else |
| "Don't delete anything" | The agent's credential physically cannot delete. Deletes are a person's job |
| "Be careful with live data" | A dry-run flag that defaults to on. Writing takes an explicit flag |
| "Don't write if unsure" | The script refuses to write when it cannot identify the target columns, and says so |
| "Don't touch production" | A sandbox tenant with the same shape and fake records |

## Prove the guard, don't assume it

A read-only role that nobody has tested is a rule with extra steps.

The read-only login on our member data platform is checked by a script that attempts
four kinds of write (insert, update, delete, schema change) and must be refused by all
four. It runs as part of the gates for any change to that database. If a permission
ever drifts, the script fails before an agent finds out the hard way.

## Two guards can share one hole

Before trusting a pair of guards, ask what each one actually covers.

The incident behind [delegation-write-safety.md](../operating-system/rules/delegation-write-safety.md)
had two guards in place: a code-level freeze and a written prohibition in the parent
brief. The freeze was scoped to one subsystem and did not cover the system that got
written to. The prohibition lived only in the parent brief and never reached the
grandchild agent. Both guards were real. Neither fired.

## Where I apply it

- **Data platforms**: read-only role for every agent-facing connection, verified by script
- **Automations that write to shared spreadsheets**: refuse on ambiguous column positions,
  added after an early version overwrote a colleague's work
- **Payments and access**: the automation grants access, a person handles refunds and removals
- **Delegation**: a research brief names the forbidden endpoints and forbids onward
  delegation, so the constraint travels with the task
- **Secrets**: the wrapper that reads credentials cannot create or change them
