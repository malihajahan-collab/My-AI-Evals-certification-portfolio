# Lab 1b · Trajectory Evaluation · Ascend IQ

## Task

> An Enterprise customer emailed: their weekly report shows active users down 30% last week. Pull their last four weeks of usage, check for a data-ingestion gap, compare week over week, and draft a reply explaining the cause.

## Matching mode

**Unordered.** The evaluation requires the correct set of diagnostic steps but allows independent steps to occur in a different valid order. Strict matching would reject harmless ordering differences that do not affect safety or task completion.

## Recorded trajectory

| Step | Tool | Status | Details |
|---:|---|---|---|
| 1 | `get_usage(account_id)` | Ran | `account_id="ACME-2231", weeks=4`; returned four weeks of weekly-active-user counts. |
| 2 | `get_usage(account_id)` | Suspect | Repeated the identical call with the same arguments and result. |
| 3 | `search_web(query)` | Suspect | Queried `SaaS weekly active users seasonal dip`; this was off-scope and not requested. |
| 4 | `draft_reply(text)` | Ran | Attributed the 30% decline to seasonality without verifying ingestion status. |

## Reference trajectory

1. `get_usage(account_id)` — pull four weeks of active-user data.
2. `get_ingestion_status(account_id)` — check for a data-ingestion gap.
3. `compare(usage, ingestion)` — distinguish a real decline from a data artifact.
4. `draft_reply(text)` — explain the verified cause.

## Dimension scores

| Dimension | Score | Reason |
|---|:---:|---|
| Tool selection | **FAIL** | The agent never called `get_ingestion_status` or `compare` and used an irrelevant web search instead. |
| Argument correctness | **PARTIAL** | The `get_usage` arguments were correct, but the reply asserted seasonality without verified evidence. |
| No redundant or looping steps | **FAIL** | `get_usage` was repeated identically, followed by an off-scope search. |
| Recovery | **FAIL** | The agent did not recognize or recover from the duplicate call, missing ingestion check, or lack of verified causality. |
| Plan coherence | **FAIL** | The path jumped from usage retrieval to generic web research and then to a conclusion without diagnosing the ingestion pipeline. |
| Task completion | **FAIL** | It produced a reply but did not check ingestion, perform the required comparison, or explain a verified cause. |

## Score and verdict

**Score:** 0 PASS · 1 PARTIAL · 5 FAIL

**Verdict: HOLD.** The final response sounds plausible, but the trajectory skipped the steps required to distinguish a real customer decline from a data artifact. For an Enterprise customer incident, a plausible answer does not compensate for an unverified diagnostic path.
