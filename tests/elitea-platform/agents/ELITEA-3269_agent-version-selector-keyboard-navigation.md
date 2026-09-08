---
id: ELITEA-3269
title: "Agent — Version Selector Keyboard Navigation"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:accessibility, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3269: Agent — Version Selector Keyboard Navigation

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the version selector dropdown supports keyboard navigation (arrow keys, Enter, Escape).

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least 4 versions
- User has keyboard access to the page

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥4 versions (base, v1, v2, v3) |
| Initial Version | base |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent page and focus on the version selector | Version selector is focused (visible focus indicator) |
| 2 | Press Enter or Space to open the dropdown | Dropdown opens |
| 3 | Press Down Arrow key | Focus moves to the next version in the list |
| 4 | Press Down Arrow key again | Focus moves to the next version |
| 5 | Press Up Arrow key | Focus moves back to the previous version |
| 6 | Press Down Arrow key until reaching the last version | Focus moves down the list; reaching the last version, focus stops or cycles to first |
| 7 | Press Up Arrow key to navigate back | Focus moves up the list |
| 8 | With a version focused, press Enter | Dropdown closes; focused version is selected and displayed |
| 9 | Reopen dropdown and press Escape | Dropdown closes without changing selection |
| 10 | Verify Tab key moves focus out of the dropdown and closes it | Dropdown closes; focus moves to next focusable element |

## Expected Final State

Keyboard navigation (arrow keys, Enter, Escape, Tab) works correctly; version can be selected via keyboard; dropdown closes on Escape and Tab.

## Pass/Fail Criteria

**Pass:** Arrow keys navigate through versions; Enter selects focused version; Escape closes dropdown without selection; Tab closes dropdown and moves focus

**Fail:** Keyboard navigation does not work; arrow keys do not move focus; Enter/Escape/Tab do not behave correctly
