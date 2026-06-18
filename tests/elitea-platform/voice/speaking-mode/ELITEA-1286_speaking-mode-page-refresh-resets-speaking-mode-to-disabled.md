---
id: ELITEA-1286
title: "Speaking Mode — Page Refresh Resets Speaking Mode to Disabled"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1286: Speaking Mode — Page Refresh Resets Speaking Mode to Disabled

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify that Speaking Mode resets to disabled after a full page refresh, ensuring the mode is not automatically re-activated on re-load.

**Coverage:** Mode ON before refresh → OFF after refresh; mic does not auto-activate.

## Preconditions

- Speaking Mode currently active on Chat page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm Speaking Mode indicator is ON. | Speaking Mode active; mic running |
| 2 | Press F5 (or browser Refresh) to reload the page. Wait for full load. | Page reloads completely |
| 3 | Observe Speaking Mode indicator after reload. | Indicator shows OFF; mic has not auto-started |

## Expected Final State

Indicator shows OFF; mic has not auto-started

## Pass/Fail Criteria

**Pass:**
- Speaking Mode indicator is OFF after full page refresh; mic has not auto-activated

**Fail:**
- Speaking Mode is still ON after refresh; mic activates automatically on page load
