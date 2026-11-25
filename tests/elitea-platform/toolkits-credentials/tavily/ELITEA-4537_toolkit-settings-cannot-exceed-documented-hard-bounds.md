---
id: ELITEA-4537
title: "Verify toolkit settings cannot be configured beyond their documented hard bounds"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid credential, attached to an agent

## Test Data

| Field | Value |
|-------|-------|
| Max Results | 50, 0, -1 |
| Natural-language over-limit request | "extract these 6 URLs: ..." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attempt to set Max Results to 50 | UI rejects/clamps the value on save, or if accepted, an actual `web_search` call never returns more than 10 results |
| 2 | Attempt to set Max Results to 0 or a negative number | UI rejects this or falls back to a valid default |
| 3 | Ask an agent (not the Test page) to extract 6 URLs via natural language | The model/toolkit still enforces the 5-URL cap end-to-end |

## Expected Final State

Hard bounds are confirmed to be enforced at the tool-execution level regardless of how the request is framed.

## Pass/Fail Criteria

**Pass:**
- No configuration or natural-language request can exceed the documented hard bounds in actual tool execution

**Fail:**
- Any bound is exceeded in actual execution, even if the originating UI/request appeared to accept it
