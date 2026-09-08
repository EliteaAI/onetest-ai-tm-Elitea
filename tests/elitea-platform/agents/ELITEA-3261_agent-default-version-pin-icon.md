---
id: ELITEA-3261
title: "Agent — Default Version Pin Icon"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3261: Agent — Default Version Pin Icon

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the default/pinned version displays an active pin icon with the correct tooltip in the Agent version selector (if default version functionality exists for Agents).

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions
- One version is set as the default/pinned version
- User has permission to view versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions |
| Default Version | production-v1 |
| Other Versions | base, staging-v2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads successfully |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions |
| 3 | Locate the default version (production-v1) in the list | production-v1 is visible in the dropdown |
| 4 | Verify an active/filled pin icon is displayed next to production-v1 | Active pin icon is visible next to production-v1 |
| 5 | Hover over the pin icon | Tooltip appears displaying "Default version" |
| 6 | Verify the pin icon is independent of the selected version indicator | If production-v1 is selected, it shows both checkmark and pin icon; if not selected, it shows only pin icon |
| 7 | Select a different version (staging-v2) | staging-v2 is now selected with checkmark |
| 8 | Reopen dropdown and verify production-v1 still shows pin icon | production-v1 displays pin icon but no checkmark (only staging-v2 has checkmark) |

## Expected Final State

Default version (production-v1) displays pin icon with "Default version" tooltip; pin icon is independent of selected version indicator.

## Pass/Fail Criteria

**Pass:** Default version displays active pin icon; tooltip shows "Default version"; pin icon persists regardless of which version is selected

**Fail:** Pin icon missing on default version; incorrect tooltip text; pin icon disappears when selecting a different version

**Note:** If default version functionality does not exist for Agents, mark this test as N/A and document findings.
