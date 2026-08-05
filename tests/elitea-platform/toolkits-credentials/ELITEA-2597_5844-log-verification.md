---
id: ELITEA-2597
title: "[EliteaAI/elitea_issues#5844] ADO Toolkit: Log Verification (LLM Call Count)"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-2597: ADO Toolkit — Log Verification (LLM Call Count)

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify LLM vision API call counts match expected caching behavior (primary proof method).

## Preconditions

- ADO toolkit configured with `process_images: true`
- LLM/tool logs capture all API calls with timestamps
- Multiple ADO items with same and different images
- Same toolkit session

## Test Data

| Scenario | Items | Images | Expected LLM Calls |
|----------|-------|--------|-------------------|
| All unique | 3 | 3 unique | 3 calls |
| With repeats | 3 | 1 repeated 3x | 1 call |
| Mixed | 3 | 2 unique | 2 calls |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Retrieve 3 ADO items, each with different image. | 3 LLM vision calls logged. |
| 2 | Verify call count = unique image count. | Log count = 3. |
| 3 | Retrieve 3 ADO items with SAME image repeated. | Only 1 LLM vision call logged. |
| 4 | Verify first call generates description; others reuse cache. | Single API request for all 3 occurrences. |
| 5 | Retrieve mix: 2 unique + 1 duplicate of first. | 2 LLM vision calls logged. |
| 6 | Verify duplicate image reuses cache (no 3rd call). | Log shows 2 calls, not 3. |
| 7 | Document actual LLM call count vs expected. | Logs confirm caching behavior. |
| 8 | Verify timestamps show first call, then reuses (no time gap for cache hits). | Timestamps confirm cache hits are instant. |

## Expected Final State

- LLM call count = unique images + unique prompts
- Log shows cache reuse behavior
- No redundant API calls for duplicates
- Timestamps confirm instant cache hits
- Primary proof of caching implementation

## Pass/Fail Criteria

**Pass:** LLM call count matches unique images; logs confirm caching; no redundant calls.  
**Fail:** LLM called for every image; duplicate images trigger new calls; logs don't match behavior.
