---
id: ELITEA-0083
title: "Configured Toolkit Appears in Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0083: Configured Toolkit Appears in Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a properly configured toolkit added to the agent appears in the `/` autosuggest dropdown.

**Coverage:** Toolkit entity type visible in autosuggest; entity type label "Toolkit" shown under the item name

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has a valid Toolkit (e.g., "Ado_repo_M") added and showing "Show tools"

## Test Data

Toolkit name: Ado_repo_M

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode and expand the Instructions section. | Instructions field is editable. |
| 2 | Click into the Instructions field and type `/`. | Autosuggest dropdown appears. |
| 3 | Inspect the dropdown list for the toolkit entry. | "Ado_repo_M" is listed with entity type label "Toolkit". |

## Expected Final State

"Ado_repo_M" is listed with entity type label "Toolkit".

## Pass/Fail Criteria

PASS: Toolkit name and "Toolkit" label are visible in the dropdown
FAIL: Toolkit does not appear in the dropdown; entity type label is missing or wrong
