---
id: ELITEA-2940
title: "Authorization details section (Toolkit server / Resource metadata / Authorization server / Scopes) expand/collapse behaves correctly"
priority: medium
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An OAuth-requiring toolkit (no valid token) can trigger the "Toolkit Authorization Required" popup

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit under test | Any OAuth-requiring toolkit (SharePoint/OpenAPI/Remote MCP) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger the popup | Popup appears with "Authorization details" collapsed by default (or in its default state) |
| 2 | Click to expand "Authorization details" | Section expands, revealing Toolkit server, Resource metadata, Authorization server, and Scopes fields correctly populated |
| 3 | Click to collapse "Authorization details" | Section collapses, hiding the fields, without affecting the rest of the popup (buttons remain visible/functional) |
| 4 | Re-expand and collapse multiple times in succession | Expand/collapse toggles reliably every time with no visual glitches or stuck states |

## Expected Final State

The Authorization details section reliably expands and collapses on demand, correctly showing/hiding all four fields, without disrupting the rest of the popup.

## Pass/Fail Criteria

**Pass:**
- Expand/collapse works reliably and repeatedly
- All four fields display correctly when expanded
- Authorize/Skip buttons remain functional regardless of expand/collapse state

**Fail:**
- Section fails to expand or collapse, or becomes stuck
- Fields are missing, mislabeled, or empty when expanded
- Expand/collapse interaction interferes with Authorize/Skip button functionality
