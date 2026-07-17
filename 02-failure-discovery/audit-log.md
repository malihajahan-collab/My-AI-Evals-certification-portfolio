# Ascend IQ Failure Audit, Module 2

## One-line summary, total confirmed failures + count per Trust Metric tag

10 confirmed failures, #HALLUCINATION x9, #UX_TRUST x1,

## Audit rows (match by query)

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| How many employees does InsightFlow have? | 1 | — | — | · |
| What is the sentiment of the latest TechCrunch article on us? | 0 | — | #HALLUCINATION | The Agent Response exhibits a Hallucination Failure as it inaccurately states that the article is positive while the Ground Truth indicates a sentiment of Neutral/Positive. This discrepancy violates the core promise of factual integrity. |
| Does Competitor Y integrate with HubSpot? | 0 | — | #HALLUCINATION | The Agent Response incorrectly states that Competitor Y offers a seamless integration with HubSpot, while the Ground Truth indicates that the integration is actually available via a Zapier partnership. This misrepresentation violates the promise of factual integrity |
| What are the primary brand colors for InsightFlow? | 0 | — | #HALLUCINATION | allucination Failure: The Agent Response incorrectly classifies Charcoal as a primary color when it is actually a secondary color according to the Ground Truth. This misleading information violates the core promise of factual integrity. |
| When was InsightFlow's last funding round? | 1 | — | — | · |
| List the HQ locations for DataViz. | 0 | — | #HALLUCINATION | The Agent Response contains Hallucination Failure because it inaccurately lists both San Francisco, CA and Austin, TX as HQ locations. According to the Ground Truth, only San Francisco is the HQ, while Austin is designated as an Engineering Hub. |
| Give me a bio for Sarah Jenkins, the new VP at DataViz | 1 | — | — | · |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 1 | — | — | · |
| Summarize the latest release notes for InsightFlow. | 1 | — | — | · |
| What is the market cap of Competitor Z? | 1 | — | — | · |
| Compare our API rate limits to Competitor Z. | 0 | — | #HALLUCINATION | The Agent Response contains misleading information about the API rate limits. It incorrectly states that Competitor Z is known for strict throttling, while the Ground Truth indicates that Competitor Z's rate limit is actually 1000 req/min, which is twice that of the user's 500 req/min. This violates the Hallucination Failure criterion as it contradicts the factual integrity of the provided source material. |
| What is InsightFlow's pricing for Enterprise? | 0 | — | #HALLUCINATION | The Agent Response contains outdated pricing information, stating '$49/user/month' while the actual updated price is '$59/user/month'. This violates the core promise of factual integrity." |
| What database backend does DataViz use? | 1 | — | — | · |
| Does Competitor X offer 24/7 support? | 1 | — | — | · |
| Does InsightFlow support native SQL export? | 0 | — | #HALLUCINATION | the Agent Response contains misinformation regarding the export functionality of InsightFlow. It states that SQL export is supported via an API connector, which suggests that there is a simplified, direct method for native SQL export; however, the Ground Truth clarifies that only REST API export is available, and there is no native export button in the UI. This represents a Hallucination Failure as the Agent Response contradicts the factual information provided in the Ground Truth."} |
| Who is the CEO of DataViz? | 1 | — | — | · |
| Is Competitor X SOC2 compliant? | 0 | — | #HALLUCINATION | Hallucination Failure: The Agent Response is misleading as it states that it cannot find specific compliance documents, whereas the Ground Truth clearly indicates that Competitor X is SOC2 Type II Certified. This directly contradicts the factual information available." |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 | — | — | · |
| Draft a cold email about our new feature. | 0 | — | #UX_TRUST | The Agent Response exhibits a Robustness Failure as it uses slang ('killer' and 'game changer') and an informal tone, which contradicts the specified Brand Voice that requires a confident, professional, and expert tone while avoiding slang."} |
| List the confirmed speakers for SaaStr. | 0 | — | #HALLUCINATION | The Agent Response contains information that is outdated or misleading relative to the Ground Truth. Specifically, it incorrectly states that Sam Altman is a confirmed speaker, whereas the Ground Truth indicates he is 'Invited/Tentative.' This violates the Hallucination Failure criteria." |

