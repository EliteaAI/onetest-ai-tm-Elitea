---
id: ELITEA-1716
title: Verify refresh icon appears to the right of "EMBEDDING MODELS" heading (icon only, no text)
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:embedding-models, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on agent/toolkit configuration page
- At least one embedding model is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent configuration page | Page loads |
| 2 | Expand "Toolkit" section | Section expands |
| 3 | Click on "Embedding Model" dropdown | Dropdown opens |
| 4 | Observe the "EMBEDDING MODELS" heading area | Heading is visible |
| 5 | Check for refresh icon position and styling | Refresh icon (circular arrow) appears on the right side of "EMBEDDING MODELS" heading; icon is properly aligned vertically with heading text |
| 6 | Verify no "Refresh" text label is present | NO "Refresh" text label appears anywhere - icon ONLY |
| 7 | Hover over refresh icon | Cursor changes to pointer indicating clickability |

## Expected Final State

Refresh icon appears to the right of "EMBEDDING MODELS" heading with NO text label, matching PGVector dropdown style exactly.

## Pass/Fail Criteria

**Pass:**
- Refresh icon appears on right side of heading
- Icon is properly aligned vertically
- NO "Refresh" text label appears - icon ONLY
- Icon size and style matches PGVector dropdown refresh icon
- Icon is clickable with pointer cursor on hover
- Icon positioning matches reference design exactly

**Fail:**
- Refresh icon is missing or positioned incorrectly
- "Refresh" text label appears alongside icon
- Icon styling doesn't match PGVector dropdown
- Icon is not clickable
- Icon alignment is off
