---
id: ELITEA-3268
title: "Agent — Version Selector Closes on Selection"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:usability, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3268: Agent — Version Selector Closes on Selection

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the version selector dropdown closes automatically after a version is selected.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least 3 versions
- User has permission to switch versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions (base, version-a, version-b) |
| Initial Version | base |
| Target Version | version-a |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent page (base version currently selected) | Agent page loads with base version |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions |
| 3 | Click on version-a to select it | Dropdown closes automatically |
| 4 | Verify the version selector button/field displays version-a | Version selector shows "version-a" |
| 5 | Reopen the version selector dropdown | Dropdown opens |
| 6 | Click on version-b to select it | Dropdown closes automatically |
| 7 | Verify the version selector displays version-b | Version selector shows "version-b" |

## Expected Final State

After each version selection, dropdown closes automatically and the selected version is displayed in the selector.

## Pass/Fail Criteria

**Pass:** Dropdown closes automatically after selecting a version; selected version is displayed in the selector

**Fail:** Dropdown remains open after selection; selected version not displayed correctly
