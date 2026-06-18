---
id: ELITEA-1169
title: "TC-006: Confluence Advanced Settings Is Collapsed by Default and Expands/Collapses on Click"
priority: critical
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1169: TC-006: Confluence Advanced Settings Is Collapsed by Default and Expands/Collapses on Click

**Module:** Confluence Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Advanced Settings" accordion in the Confluence toolkit form is collapsed by default on form open, expands when clicked, and collapses again on a second click. Arrow indicator must visually reflect the current state.

Coverage:
- Advanced Settings collapsed by default
- Arrow indicator (▶) when collapsed
- Click expands; arrow changes to (▼)
- Click again collapses; arrow reverts to (▶)

## Preconditions

- Logged in as User A
- Confluence toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Confluence toolkit creation form | Form renders; Advanced Settings section is visible as a collapsed header below the main fields |
| 2 | Observe Advanced Settings before interaction | Section is collapsed; advanced fields (Max Pages, Number of Retries, Min/Max Retry Seconds, Custom Headers) are NOT visible; arrow indicator points right (▶) |
| 3 | Click the 'Advanced Settings' header | Section expands; all advanced fields become visible |
| 4 | Observe the arrow indicator after expanding | Arrow now points down (▼) |
| 5 | Click 'Advanced Settings' header again | Section collapses; advanced fields hidden; arrow reverts to ▶ |

## Expected Final State

Section collapses; advanced fields hidden; arrow reverts to ▶

## Pass/Fail Criteria

PASS:
- Section is collapsed by default on form open
- Arrow changes on expand/collapse
- One click expands; second click collapses

FAIL:
- Section is expanded on form open
- Clicking has no effect
- Section expands but cannot be collapsed
