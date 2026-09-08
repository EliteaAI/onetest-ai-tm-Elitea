---
id: ELITEA-3267
title: "Agent — Version Selector Closes on Outside Click"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:usability, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3267: Agent — Version Selector Closes on Outside Click

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the version selector dropdown closes when the user clicks outside of it.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥2 versions |
| Outside Click Targets | Page header, sidebar, main content area |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads |
| 2 | Open the version selector dropdown | Dropdown opens and remains open |
| 3 | Click on the page header area (outside dropdown) | Dropdown closes immediately |
| 4 | Reopen the version selector dropdown | Dropdown opens |
| 5 | Click on the sidebar navigation (outside dropdown) | Dropdown closes immediately |
| 6 | Reopen the version selector dropdown | Dropdown opens |
| 7 | Click on the main content area (outside dropdown, e.g., system prompt field) | Dropdown closes immediately |
| 8 | Verify the dropdown does not close when clicking inside the dropdown area | Clicking inside dropdown (on search field, scrollbar, version rows) keeps dropdown open |

## Expected Final State

Dropdown closes when clicking outside; remains open when clicking inside.

## Pass/Fail Criteria

**Pass:** Dropdown closes on any click outside the dropdown area; remains open when clicking inside

**Fail:** Dropdown does not close on outside click; dropdown closes on inside click
