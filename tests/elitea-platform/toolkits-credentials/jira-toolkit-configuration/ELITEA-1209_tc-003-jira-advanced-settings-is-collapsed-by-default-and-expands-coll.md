---
id: ELITEA-1209
title: "TC-003: Jira Advanced Settings Is Collapsed by Default and Expands/Collapses on Click"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1209: TC-003: Jira Advanced Settings Is Collapsed by Default and Expands/Collapses on Click

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Advanced Settings" accordion section exists in the Jira toolkit form, is collapsed by default on form open, expands when clicked to reveal all advanced fields, and collapses again when clicked a second time.

Coverage:
- "Advanced Settings" section present and collapsed by default on form open
- Expand arrow indicator points right (▶) when collapsed
- Clicking expands section and shows all advanced fields
- Arrow indicator points down (▼) when expanded
- Clicking again collapses the section; arrow reverts to ▶

## Preconditions

- Logged in as User A
- Jira toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira toolkit creation form | Form renders; Advanced Settings section is visible as a collapsed header |
| 2 | Observe the 'Advanced Settings' section before clicking | Section is collapsed — Verify SSL, Additional Fields, Custom Headers are NOT visible; arrow indicator points right (▶) |
| 3 | Click the 'Advanced Settings' header/row | Section expands; Verify SSL, Additional Fields, and Custom Headers are now visible |
| 4 | Observe the arrow indicator after expanding | Arrow now points down (▼) indicating expanded state |
| 5 | Click 'Advanced Settings' again | Section collapses; Verify SSL, Additional Fields, Custom Headers are hidden again; arrow reverts to ▶ |

## Expected Final State

Section collapses; Verify SSL, Additional Fields, Custom Headers are hidden again; arrow reverts to ▶

## Pass/Fail Criteria

PASS:
- Advanced Settings exists and is collapsed on form open
- One click expands it; another click collapses it
- Arrow indicator changes direction to reflect state

FAIL:
- Advanced Settings section is missing from the form
- Advanced Settings is expanded by default (not collapsed)
- Clicking has no effect or section expands but cannot be collapsed
