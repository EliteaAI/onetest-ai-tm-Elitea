---
id: ELITEA-4523
title: "Verify boundary values (exact ceiling, zero, negative, non-integer) are handled correctly for every numeric tool parameter"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid API key, open on its "Test Toolkit" page

## Test Data

| Field | Boundary values tested |
|-------|-------------------------|
| Web crawl Max Depth | 2 (succeeds), 3 (rejected) |
| Web crawl Limit | 20 (succeeds), 21 (rejected) |
| Web map Limit | 50 (succeeds), 51 (rejected) |
| Web map Max Depth | 2 (succeeds), 3 (rejected) |
| Any numeric field | 0, -1, "abc", 1.5 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Web crawl Max Depth to exactly 2, then to 3 | 2 succeeds; 3 is rejected |
| 2 | Set Web crawl Limit to exactly 20, then 21 | 20 succeeds; 21 is rejected |
| 3 | Set Web map Limit to exactly 50, then 51 | 50 succeeds; 51 is rejected |
| 4 | Set Web map Max Depth to exactly 2, then 3 | 2 succeeds; 3 is rejected |
| 5 | Enter 0 into a numeric field (e.g. Max Depth or Limit) | A clear validation message is shown, or the value is sensibly rejected — never a silent no-op or crash |
| 6 | Enter -1 into the same field | Same graceful handling as zero |
| 7 | Attempt to type "abc" directly into the field | Field prevents non-numeric characters entirely, or shows a clear validation message rather than allowing a broken submission |
| 8 | Enter 1.5 where an integer is expected | Value is rejected or predictably rounded, not silently truncated in a misleading way |

## Expected Final State

Every numeric parameter's exact ceiling and invalid-type edge cases behave predictably.

## Pass/Fail Criteria

**Pass:**
- Exact ceilings succeed and one-above-ceiling values fail
- Zero/negative/non-numeric/decimal input is handled gracefully everywhere

**Fail:**
- An exact ceiling incorrectly fails, or one-above-ceiling incorrectly succeeds
- Any invalid-type input causes a crash, silent no-op, or misleading truncation
