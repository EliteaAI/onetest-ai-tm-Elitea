---
id: ELITEA-3260
title: "Agent — Selected Version Indicator"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3260: Agent — Selected Version Indicator

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the currently selected version is clearly indicated with a checkmark icon and row highlight in the version selector dropdown.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least 3 versions
- User has permission to view and switch versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions (base, version-a, version-b) |
| Initial Version | base |
| Target Version | version-a |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent page (base version is currently selected) | Agent page loads with base version displayed in selector |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions |
| 3 | Locate the currently selected version (base) in the list | base version row displays a checkmark icon |
| 4 | Verify the currently selected version row has visual highlighting | base version row has distinct background color or border highlighting |
| 5 | Click on version-a to select it | Dropdown closes; version-a is now displayed in the selector |
| 6 | Reopen the version selector dropdown | Dropdown opens |
| 7 | Verify version-a now shows the checkmark icon and row highlight | version-a displays checkmark and visual highlighting |
| 8 | Verify base no longer shows the checkmark or highlight | base version row has no checkmark and no highlighting |

## Expected Final State

Only version-a displays checkmark and highlight; base version has no checkmark or highlight.

## Pass/Fail Criteria

**Pass:** Selected version always displays checkmark + row highlight; previously selected version loses both indicators when a new version is selected

**Fail:** Checkmark or highlight missing on selected version; multiple versions show checkmark; previous version retains checkmark after switching
