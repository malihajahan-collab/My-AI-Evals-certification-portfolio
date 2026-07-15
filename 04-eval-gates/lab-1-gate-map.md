# Eval Gates & Thresholds

> Module 4 · Eval Gates · repo file; feeds the Eval Gates slide of your final pitch deck
>
> Where your eval suite plugs into the delivery lifecycle, and the thresholds that decide ship / hold.

## 1. Gate placement

_Where in the lifecycle does each gate sit, and what does it block?_

| Gate | Lifecycle stage (PR / pre-deploy / canary / prod monitor) | What it blocks |
|---|---|---|
| _…_ | _…_ | _…_ |

## 2. Thresholds

_The exact pass bar at each gate. Be specific, these are the numbers a release rides on._

| Metric | Gate | Threshold | If it fails… |
|---|---|---|---|
| _…_ | _…_ | _…_ | _block / warn / rollback_ |

## 3. Human-in-the-loop

_Which decisions require a human, and who is that human? What do they see?_

## 4. Launch strategy

_How do you roll out behind these gates? (shadow → canary % → full). What signal promotes each stage?_

## 5. Rollback & kill-switch

_What triggers a rollback, and how fast can you pull the feature?_

## 6. Trade-off justification

_Why these thresholds? What's the cost of too-strict (blocks good releases) vs too-loose (ships failures)?_
