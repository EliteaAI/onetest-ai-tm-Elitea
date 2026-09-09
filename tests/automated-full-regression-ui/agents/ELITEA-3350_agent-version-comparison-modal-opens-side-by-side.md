---
id: ELITEA-3350
title: "Agent Version Comparison Modal Opens with Side-by-Side Layout"
priority: critical
type: regression
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, regression, version-comparison, story:6304]
requirements: [EliteaAI/elitea_issues#6304]
---
# ELITEA-3350: Agent Version Comparison Modal Opens with Side-by-Side Layout

**Module:** Agents · **Priority:** Critical · **Type:** Regression

**Objective:** Verifies that the version comparison modal opens successfully and displays two agent versions side-by-side with correct version names in column headers and functional close controls.

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Test agent exists with at least 2 versions (base version + 1 named version)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Agent | Agent with 2+ versions |
| Version 1 | base |
| Version 2 | v1.0 (or any named version) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to test agent details page | Agent page loads successfully |
| 2 | Verify agent has 2+ versions in version selector dropdown | Version selector shows multiple versions |
| 3 | Click "Compare Versions" button in actions menu | Compare Versions button is visible and clickable |
| 4 | Verify modal opens without errors | Modal opens and renders successfully |
| 5 | Verify modal displays two version columns side-by-side | Two columns visible with equal or proportional width |
| 6 | Verify left column header shows actual version name (e.g., "base") | Left column labeled with correct version name (not "Version A") |
| 7 | Verify right column header shows actual version name (e.g., "v1.0") | Right column labeled with correct version name (not "Version B") |
| 8 | Verify modal has X close button in top-right corner | Close button (X icon) is visible and accessible |
| 9 | Verify Cancel or Close action button exists at bottom of modal | Cancel/Close button present in modal footer |
| 10 | Click X button to close modal | Modal closes successfully and returns to agent details page |
| 11 | Reopen modal and click Cancel button | Modal closes successfully via Cancel button |
| 12 | Verify no console errors or visual glitches during open/close operations | No JavaScript errors; smooth modal transitions |

## Expected Final State

Version comparison modal opens displaying two agent versions side-by-side with actual version names in headers, functional X and Cancel buttons, and no errors.

## Pass/Fail Criteria

**Pass:**
- Modal opens successfully on Compare Versions button click
- Two version columns displayed side-by-side (not stacked)
- Column headers show actual version names from agent (e.g., "base", "v1.0")
- Modal can be closed via both X button and Cancel button
- No console errors or UI glitches

**Fail:**
- Modal fails to open or displays errors
- Columns not displayed side-by-side (vertical stack or single column)
- Generic labels used instead of version names ("Version A", "Version B")
- Cannot close modal via X or Cancel button
- Console errors or broken UI elements
