# Launch Strategy

> Module 4 · Eval Gates · repo file; the rollout plan behind your Eval Gates slide
>
> How the gate policy in `lab-1-gate-map.md` translates into a safe release: staged rollout, monitoring, and the conditions under which you'd roll back.

## Rollout stages

| Stage | Audience / % traffic | Gate that must pass to advance | Monitoring signal |
|---|---|---|---|
| _e.g. internal_ | _…_ | _…_ | _…_ |
| _e.g. canary_ | _…_ | _…_ | _…_ |
| _e.g. GA_ | _…_ | _…_ | _…_ |

## Rollback triggers

_What live signal (per-dimension regression, incident, threshold breach) forces a hold or rollback, and who makes the call?_

## Risk tolerance

_Which dimensions block a launch outright vs. warn-and-proceed, and why that's acceptable for this feature._
