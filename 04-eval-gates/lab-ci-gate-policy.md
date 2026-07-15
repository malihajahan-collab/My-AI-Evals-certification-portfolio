# CI Eval Gate Policy

> Module 4 · Eval Gates · repo file; the enforceable policy behind your Eval Gates slide
>
> How your eval suite actually blocks a bad change in CI: which dimensions gate a PR, the thresholds, and how you replay against a frozen regression set. Pairs with `lab-1-gate-map.md`.

## Gate policy

| Dimension | Threshold | Blocks PR? | Rationale |
|---|---|---|---|
| _e.g. factuality_ | _…_ | _yes / warn_ | _…_ |
| _e.g. safety_ | _…_ | _…_ | _…_ |

## Regression golden set

- **Size (frozen cases):** _≥ 30_
- **How it's replayed on each PR:** _…_
- **When the set gets updated:** _…_

## Ownership

_Who owns the gate policy, who can change thresholds, and who is on-call when the gate fires._
