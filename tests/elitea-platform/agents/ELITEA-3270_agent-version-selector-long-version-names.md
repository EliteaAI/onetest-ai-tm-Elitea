---
id: ELITEA-3270
title: "Agent — Version Selector Long Version Names"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:ui-robustness, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3270: Agent — Version Selector Long Version Names

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that long version names do not break the UI layout or cause overflow issues.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least one version having a very long name (≥50 characters)
- User has permission to create and view versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with multiple versions |
| Long Version Name | "production-release-candidate-v2-with-security-fixes-2026-01-15-final" (≥50 chars) |
| Other Versions | base, short-v1 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new version with the long name (if not already created) | Version created successfully |
| 2 | Navigate to the Agent configuration page | Agent page loads |
| 3 | Open the version selector dropdown | Dropdown opens showing all versions |
| 4 | Locate the version with the long name | Long version name is visible in the list |
| 5 | Verify the long version name is displayed without breaking the layout | Text wraps or truncates appropriately (ellipsis if truncated) |
| 6 | Verify metadata (timestamp, creator) remains visible and aligned | Timestamp and creator info are visible and properly positioned |
| 7 | Verify icons (checkmark, pin if applicable) remain properly positioned | Icons are aligned correctly, not overlapped by text |
| 8 | Hover over the truncated name (if applicable) | Tooltip appears showing the full version name |
| 9 | Select the long-named version | Version is selected; selector displays the name (truncated if necessary) |

## Expected Final State

Long version name displays without breaking layout; text wraps or truncates with ellipsis; tooltip shows full name; metadata and icons remain visible and aligned.

## Pass/Fail Criteria

**Pass:** Long name does not break layout; wraps or truncates gracefully; tooltip shows full name; metadata and icons properly positioned

**Fail:** Layout breaks; text overflows; metadata or icons misaligned or hidden; no tooltip for truncated text
