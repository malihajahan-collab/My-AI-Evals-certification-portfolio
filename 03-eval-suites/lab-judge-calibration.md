# Judge Calibration (κ)

> Module 3 · Eval Suites · repo file; the "can we trust the judge?" evidence behind your Eval Results slide
>
> An LLM-as-a-Judge is only useful if it agrees with a human. This captures how well your judge matches your own labels, measured with Cohen's κ.

## Calibration run

- **Sample size (labeled cases):** _…_
- **Cohen's κ (judge vs your labels):** _target ≥ 0.6_
- **Family separation check:** _judge model ≠ model under test, to avoid self-preference bias_

## Disagreements

_Where did the judge and your labels diverge? What pattern explains it?_

| Case | Your label | Judge label | Why they differed |
|---|---|---|---|
| _…_ | _…_ | _…_ | _…_ |

## Rubric changes

_What you changed in the judge prompt / rubric to raise κ, and the κ before vs after._
