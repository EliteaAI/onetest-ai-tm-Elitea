---
id: ELITEA-3259
title: "Agent — Version Selector Displays All Versions"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3259: Agent — Version Selector Displays All Versions

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the version selector dropdown opens successfully and displays all existing versions (base, draft, published) without errors for Agents.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- User has Editor/Admin role with appropriate permissions
- Private project context selected
- Agent exists with multiple versions (base, at least 2 draft named versions, at least 1 published version)

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥4 versions (1 base + 2 draft + 1 published) |
| Expected Versions | base, draft-v1, draft-v2, published-v1 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads successfully |
| 2 | Locate the version selector component in the page header | Version selector displays the current version name |
| 3 | Click the version selector dropdown | Dropdown opens without errors; no console errors appear |
| 4 | Count the number of versions displayed in the dropdown list | All versions are listed (4 versions: base, draft-v1, draft-v2, published-v1) |
| 5 | Verify each version displays correctly with its name visible | Each version name is clearly visible and readable |

## Expected Final State

Version selector dropdown displays all 4 versions (base, draft-v1, draft-v2, published-v1) without errors.

## Pass/Fail Criteria

**Pass:** Dropdown opens without errors; all 4 versions are listed and visible

**Fail:** Dropdown fails to open; missing versions; console errors occur
