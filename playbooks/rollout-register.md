# Rollout register: "Adopted" is the finish line

Pushing an AI tool to a team is not the same as the team using it. Most AI rollouts
die between those two points, and nobody notices because "rolled out" got ticked.

So every AI tool, skill, automation and knowledge base in the business sits in one
register, and the finish line is a status called Adopted. Rolled out is a waypoint.

## The eight statuses

```
Triage → Won't do
       → Queued → In progress → In repo → Rolled out → Adopted → Retired
```

| Status | Means |
|---|---|
| Triage | Someone suggested it. Nobody has decided yet |
| Won't do | Decided against, with a one-line reason kept |
| Queued | Yes, but not started |
| In progress | Being built |
| In repo | Built, merged, not yet in anyone's hands |
| Rolled out | Installed for the people who need it, with a how-to |
| Adopted | Those people use it without being reminded |
| Retired | Replaced or no longer needed. Kept in the register, not deleted |

## Escalation cadence

The register only works if something forces items to move.

- Anything in **Triage** over two weeks gets decided. Yes or Won't do.
- Anything **In progress** across two review cycles gets unblocked or dropped.
- Anything **Rolled out** for a month gets checked for real use. Used: Adopted.
  Not used: find out why, then fix or Retire.

## Two intake streams, because they fail differently

New capability arrives two ways, and each fails in its own way.

1. **Live sessions and announcements** are event driven. They fail loudly. You know
   you missed the call.
2. **Libraries that are quietly kept up to date** fail silently. Nothing announces the
   change, so the library drifts ahead of your register and you find out months later.

The fix for the silent one is a monthly audit with a written template: what changed
upstream, what is now in the register, what the gap is. A calendar entry with an owner,
because a stale register fails the same silent way.

## Catalogue before you build

Implementing in discovery order is how you end up having built the four easiest things
and none of the three that mattered. Get the whole list into Triage first. Then decide.
