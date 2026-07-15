# Eval Spec

> Module 3 · Eval Suites · repo file; backs the Eval Results slide of your final pitch deck
>
> The design of your automated evaluation suite: the datasets, evaluators, and pass criteria that turn your taxonomy into a repeatable test.

## 1. Datasets

_What examples does the suite run against, and where do they come from?_

| Dataset | Purpose | # examples | Source |
|---|---|---|---|
| _Golden set_ | _known-good reference cases_ | _…_ | _…_ |
| _Failure set_ | _cases that previously broke_ | _…_ | _…_ |
| _Edge set_ | _adversarial / rare inputs_ | _…_ | _…_ |

## 2. Evaluators

_One row per evaluator. Tie each back to a failure mode from Module 2._

| Evaluator | Type (code / LLM-judge / human) | Failure mode it catches | Output (score / pass-fail) |
|---|---|---|---|
| _…_ | _…_ | _…_ | _…_ |

## 3. LLM-as-judge prompts (if used)

_Paste the judge prompt(s). Note how you calibrated them against human labels._

```
[judge prompt here]
```

## 4. Pass criteria

_What score/threshold per evaluator counts as a pass? What's the aggregate bar for the suite?_

## 5. How to run it

_Commands / steps to reproduce the suite (LangSmith experiment, script, etc.)._

## 6. Baseline results

_First run of the suite against current production. Where does it stand today?_

| Evaluator | Score | Pass? |
|---|---|---|
| _…_ | _…_ | _…_ |
