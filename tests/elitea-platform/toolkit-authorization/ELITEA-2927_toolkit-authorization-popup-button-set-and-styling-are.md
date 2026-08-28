---
id: ELITEA-2927
title: "Toolkit-authorization popup button set and styling are consistent with the Sensitive Action Authorization card"
priority: high
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A sensitive-action-gated tool call can be triggered to open a Sensitive Action Authorization dialog (`ChatHitlActions`)
- An OAuth-requiring toolkit (no valid token) can be triggered to open the Toolkit Authorization Required popup

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Reference pattern | Sensitive Action Authorization dialog (`ChatHitlActions`) |
| Under test | Toolkit Authorization Required popup |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a Sensitive Action Authorization dialog and note header style, button set (Authorize/Block/Block with Comment), and layout | Baseline recorded |
| 2 | Trigger the Toolkit Authorization Required popup and note header style, button set, and layout | Popup content recorded |
| 3 | Compare the two side by side | Header style and layout align per the finalized design; button set differences (if any, e.g. Authorize/Skip) are intentional and documented, not accidental styling drift |

## Expected Final State

The Toolkit Authorization Required popup's visual style and layout align with the Sensitive Action Authorization card per the finalized design intent of the issue.

## Pass/Fail Criteria

**Pass:**
- Header style, spacing, and overall layout match the Sensitive Action Authorization card pattern
- Any button-set differences match the finalized, documented design (not unstyled/inconsistent leftovers)

**Fail:**
- Toolkit-authorization popup retains clearly mismatched or inconsistent styling versus the Sensitive Action card
- Button labels/layout appear unintentionally inconsistent (e.g. different fonts, spacing, or alignment with no design rationale)
