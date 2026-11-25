---
id: ELITEA-4529
title: "Verify Max Search Depth toolkit setting governs per-call search depth and the basic/advanced cost tradeoff"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid credential, usable from an agent or the Test page

## Test Data

| Field | Value |
|-------|-------|
| Max Search Depth | basic, advanced |
| Query | A topic benefiting from deeper research (e.g. a nuanced/recent news topic) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With Max Search Depth="basic", run the query and note the results | Results returned successfully |
| 2 | Change Max Search Depth to "advanced", re-run the identical query | Toolkit still runs successfully; compare result quality/breadth qualitatively |
| 3 | With the toolkit set to "basic", attempt to request "advanced" on a single Test-page call | The toolkit either coerces the request back to basic or rejects it — a user cannot bypass the toolkit's own cost-control setting per call |
| 4 | Leave Max Search Depth at its default ("basic") | The higher "advanced" cost is never silently incurred without explicit toolkit-owner opt-in |

## Expected Final State

Max Search Depth is confirmed as the governing ceiling for per-call depth and its associated cost tradeoff.

## Pass/Fail Criteria

**Pass:**
- The ceiling enforces basic/advanced correctly and is never silently bypassed

**Fail:**
- A per-call request exceeds the toolkit's configured ceiling
