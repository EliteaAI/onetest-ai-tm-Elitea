---
id: ELITEA-4512
title: "Verify web_search Search Depth (basic vs advanced) changes result depth and respects the toolkit's Max Search Depth ceiling"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential and Max Search Depth set to "advanced", usable from the Test page or an agent

## Test Data

| Field | Value |
|-------|-------|
| Nuanced query | A multi-faceted question (e.g. comparing two countries' policies) |
| Trivial query | A simple factual question (e.g. "capital of France") |
| Search Depth values | basic, advanced, unset/default |
| Toolkit Max Search Depth | advanced (for steps 1-2, 4-5), basic (for step 3) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the nuanced query at Search Depth "basic", then again at "advanced" (toolkit ceiling = advanced) | "Advanced" returns qualitatively deeper/more relevant content, not just a reordering |
| 2 | Run the trivial query at both depths | Both succeed and return correct results; document any meaningful difference (may be none) |
| 3 | Set the toolkit's Max Search Depth to "basic" and request "advanced" on a single call; repeat the step-1 comparison | The actual depth used is capped at basic — the "advanced"-requested result is indistinguishable in depth from a basic call |
| 4 | Leave Search Depth unset on a call | Behavior matches "basic" by default |
| 5 | Run the same "advanced" query twice in a row | Results are reasonably consistent, not wildly random |

## Expected Final State

Search Depth is confirmed as a real functional lever, and the toolkit-level ceiling is confirmed to be enforced in substance.

## Pass/Fail Criteria

**Pass:**
- "Advanced" produces deeper results than "basic" when the ceiling allows it
- The ceiling genuinely caps per-call depth when set to "basic"

**Fail:**
- "Advanced" and "basic" are indistinguishable when the ceiling allows advanced
- A per-call "advanced" request bypasses a "basic" ceiling
