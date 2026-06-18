---
id: ELITEA-1032
title: "Resources and Notifications: Create Button Expected State Verification"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1032: Resources and Notifications: Create Button Expected State Verification

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Create button state on Resources and Notifications sections, confirming whether it is absent, disabled, or shows a specific behavior per design.

**Coverage:**
- Create button on Resources page
- Create button on Notifications page

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in expanded state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Resources from the sidebar | Resources page loads |
| 2 | Inspect the Create button in the sidebar | Note current state: label, style (split or dropdown), or if absent/disabled |
| 3 | Click the button (if present) | Dropdown opens or appropriate action occurs per design; no errors thrown |
| 4 | Navigate to Notifications | Notification Center loads |
| 5 | Inspect the Create button | Note state: label, style, or absence |
| 6 | Click if present | Behavior matches design expectation; no errors |

## Expected Final State

Behavior matches design expectation; no errors

## Pass/Fail Criteria

**Pass:**
- Create button behavior on Resources and Notifications matches the Figma-defined expectation for these sections

**Fail:**
- Create button is present with an entity-specific label on sections that should not have entity creation
- Button throws errors or breaks when clicked on these pages
