---
id: ELITEA-3258
title: "Regression: Enable/Disable toggle behavior unchanged"
priority: high
type: regression
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:project-setup, project-context-builder, regression, toggle]
requirements: [EliteaAI/elitea_issues#6344]
automation_test_id:
automation_pr:
---

# ELITEA-3258: Regression: Enable/Disable toggle behavior unchanged

**Module:** settings · **Priority:** high · **Type:** regression

**Objective:** Verify that the Project Context enable/disable toggle correctly controls whether context is injected, same as before the enhancement.

---

## Preconditions

- User is logged in with Editor or Admin role
- Project Context page is accessible
- Some content exists in Project Context

---

## Test Data

| Field | Value |
|-------|-------|
| Existing content | Any project context content |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Page loads |
| 2 | If toggle is OFF, turn it ON | Toggle changes to ON |
| 3 | Open Chat and verify context is applied | AI references context |
| 4 | Return to Settings → Project Context | Page loads |
| 5 | Turn toggle OFF | Toggle changes to OFF |
| 6 | Open Chat and verify context is NOT applied | AI does not use context |
| 7 | Verify message indicates context is disabled | UI shows context disabled state |

---

## Expected Final State

The Project Context enable/disable toggle correctly controls whether context is injected, same as before the enhancement.

---

## Pass/Fail Criteria

**Pass:**
- Toggle ON: context is injected into conversations
- Toggle OFF: context is not injected
- Toggle state persists
- UI indicates current state correctly

**Fail:**
- Toggle doesn't affect context injection
- Toggle state doesn't persist
- UI state doesn't match actual behavior
