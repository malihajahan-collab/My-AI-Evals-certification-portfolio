# Module 4 · Eval Gate Map · Ascend IQ Copilot

_Generated from the M4 Eval Gate Mapping Tool._

## Context

Eng flagged 5 verified failures in the Ascend IQ data log. (Row 14, refused legal query, was correctly Pass and is not mapped.) Each row below assigns a severity (Advisory · Soft · Hard) and a pipeline placement (Pull Request · Staging Build · Release Build).

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 01 | Hallucination · Stale Pricing | 🔴 Hard | Staging Build | Unsupported pricing can cause underquoting, lost revenue, failed sales, customer disputes, and misleading-pricing exposure. Because pricing errors can directly affect purchasing decisions, critical contradictions must block promotion. |
| 17 | Tone · Slang Detected | 🔵 Advisory | Pull Request | Repeated off-brand language can weaken enterprise credibility, reduce sales-message conversion, and gradually erode customer trust. Because ordinary slang presents limited immediate harm, it should generate an advisory warning rather than block release. |
| 05 | Hallucination · False Promise | 🔴 Hard | Staging Build | Inventing confirmed speakers or commitments can force public corrections, damage partner relationships, trigger customer complaints, and erode brand trust. Externally published confirmation claims must be supported by authoritative evidence. |
| 08 | Hallucination · Contradicts Specs | 🔴 Hard | Staging Build | Unsupported negative claims about a named competitor can create false-advertising or defamation exposure, competitor disputes, legal rev costs, and reputational damage. Unsupported comparative claims should block promotion. |
| 03 | Latency · Exceeded Max Threshold | 🟡 Soft | Staging Build | Sustained response delays can increase abandonment, reduce feature adoption and task completion, raise support costs, breach enterprise service expectations, and contribute to churn. Occasional complex requests may use a documented exception threshold. |

## Sample Interactions (for reference)

**Row 01 · Hallucination · Stale Pricing**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- Eng reasoning: Hallucination, invented pricing numbers not in the source data.

**Row 17 · Tone · Slang Detected**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature, it's a total game changer for your stack!
- Eng reasoning: Tone, slang violates brand-voice guidelines.

**Row 05 · Hallucination · False Promise**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- Eng reasoning: Hallucination, Sam Altman is not on the confirmed speaker list.

**Row 08 · Hallucination · Contradicts Specs**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- Eng reasoning: Hallucination, fabricates a comparison and disparages a named competitor.

**Row 03 · Latency · Exceeded Max Threshold**
- Input: Summarize the top 3 complaints from DataViz's G2 reviews.
- Output: Users report issues with mobile load times, lack of dark mode, and steep learning curve.
- Eng reasoning: Latency, response time exceeded the max threshold (4.2s vs target 2.0s).

---

_Lab artifact for Module 4, AI Evals Certification, Product School._
