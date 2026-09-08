---
id: ELITEA-3251
title: "Regression: Enable/Disable toggle behavior unchanged"
priority: high
type: regression
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, story:6344, r-2.0.6, project-context-builder, regression, toggle]
requirements: [EliteaAI/elitea_issues#6344]
---

# ELITEA-3251: Regression: Enable/Disable toggle behavior unchanged

## Preconditions

- User has Editor or Admin role
- Project Context page accessible
- Some content exists in Project Context

## Test Data

| Field | Value |
|-------|-------|
| Existing content | Any project context content |

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

## Expected Final State

The Project Context enable/disable toggle correctly controls whether context is injected, same as before the enhancement.

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
