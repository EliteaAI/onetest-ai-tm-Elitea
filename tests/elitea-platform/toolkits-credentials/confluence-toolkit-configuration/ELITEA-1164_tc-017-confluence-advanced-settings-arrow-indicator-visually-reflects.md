---
id: ELITEA-1164
title: "TC-017 (Confluence): Advanced Settings Arrow Indicator Visually Reflects Collapse/Expand State"
priority: medium
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1164: TC-017 (Confluence): Advanced Settings Arrow Indicator Visually Reflects Collapse/Expand State

**Module:** Confluence Toolkit Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the expand/collapse arrow indicator in the Advanced Settings section accurately and consistently reflects the current state (▶ = collapsed, ▼ = expanded) for the Confluence toolkit form. This visual cue is critical for user orientation.

Coverage:
- Arrow shows ▶ when collapsed; ▼ when expanded
- Arrow changes immediately on click without lag
- Arrow state is consistent after multiple toggle cycles

## Preconditions

- Logged in as User A
- Confluence toolkit configuration form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Confluence toolkit form | Advanced Settings visible as collapsed header |
| 2 | Observe arrow indicator before clicking | Arrow points right (▶) |
| 3 | Click Advanced Settings to expand | Section expands; arrow changes to (▼) immediately |
| 4 | Click Advanced Settings again to collapse | Section collapses; arrow reverts to (▶) immediately |
| 5 | Repeat expand/collapse 3 more times | Arrow direction consistently matches the section state on every cycle; no lag or mismatch observed |

## Expected Final State

Arrow direction consistently matches the section state on every cycle; no lag or mismatch observed

## Pass/Fail Criteria

PASS:
- Arrow consistently shows correct direction for both collapsed and expanded states
- Arrow changes direction on every toggle click without lag or mismatch

FAIL:
- Arrow does not change direction when section toggles
- Arrow shows wrong direction (▼ when collapsed, ▶ when expanded)
- Arrow change is delayed or inconsistent
