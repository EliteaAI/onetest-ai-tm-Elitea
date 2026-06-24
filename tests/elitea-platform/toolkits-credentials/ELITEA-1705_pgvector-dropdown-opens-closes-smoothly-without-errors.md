---
id: ELITEA-1705
title: Verify dropdown opens/closes smoothly without errors
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, nfr:ui, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on agent/toolkit configuration page
- At least one PGVector credential exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent configuration page | Page loads |
| 2 | Expand "Toolkit" section | Section expands |
| 3 | Click on "Pgvector Configuration" dropdown to open it | Dropdown opens smoothly without lag or flickering; all credentials display correctly |
| 4 | Click outside the dropdown to close it | Dropdown closes properly |
| 5 | Click on the dropdown again to reopen | Dropdown reopens without issues |
| 6 | Press ESC key | Dropdown closes |
| 7 | Repeat open/close cycle 3-5 times | Dropdown remains functional; no visual glitches occur |

## Expected Final State

PGVector dropdown opens and closes smoothly without any UI issues or JavaScript errors.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens smoothly without lag or flickering
- Dropdown displays credentials correctly on each open
- Clicking outside closes dropdown properly
- ESC key closes dropdown
- No visual glitches during transitions
- Dropdown remains functional after multiple cycles
- No JavaScript errors in console

**Fail:**
- Dropdown is slow, laggy, or flickers
- Dropdown doesn't close properly
- ESC key doesn't work
- Visual glitches appear
- JavaScript errors occur
