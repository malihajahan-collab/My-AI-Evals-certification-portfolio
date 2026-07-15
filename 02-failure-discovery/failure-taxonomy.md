# Failure Taxonomy

> Module 2 · Failure Discovery · repo file; feeds the Failure Taxonomy slide of your final pitch deck
>
> The structured catalogue of how your feature actually breaks, built from auditing real outputs, not guesses.

## 1. Audit method

_How did you gather failures? (e.g. reviewed N real traces in LangSmith, ran adversarial prompts, mined support tickets.)_

- **Sample size:** _…_
- **Source of examples:** _…_

## 2. Failure modes

_Group the failures into named, distinct categories. Each should be observable and countable._

| Failure mode | Description | Example (input → bad output) | Frequency | Severity |
|---|---|---|---|---|
| _…_ | _…_ | _…_ | _…_ | _low / med / high_ |
| _…_ | _…_ | _…_ | _…_ | _…_ |

## 3. Severity × frequency map

_Which modes are high-severity AND common? Those drive your eval suite priorities._

## 4. Root-cause hypotheses

_For the top failure modes, what's likely causing them? (prompt, retrieval, model, data, edge case…)_

## 5. What this means for evals

_Which failure modes must your Module 3 eval suite catch? Rank them._
