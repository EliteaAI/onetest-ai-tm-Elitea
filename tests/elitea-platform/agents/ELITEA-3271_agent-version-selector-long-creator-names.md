---
id: ELITEA-3271
title: "Agent — Version Selector Long Creator Names"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:ui-robustness, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3271: Agent — Version Selector Long Creator Names

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that long creator names or email addresses do not break the UI layout.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with at least one version created by a user with a very long name or email address
- If test data is not available, create a version with a mock user having a long name

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with multiple versions |
| Long Creator Name | "Christopher Alexander Montgomery-Wellington III" (very long name) |
| Long Creator Email | "christopher.montgomery-wellington@verylongdomainname.example.com" (very long email) |
| Other Versions | Created by users with normal-length names |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions |
| 3 | Locate the version created by the user with long name/email | Version is visible in the list |
| 4 | Verify the creator information is displayed without breaking the layout | Creator name/email wraps or truncates appropriately |
| 5 | Verify other metadata (version name, timestamp) remains visible and aligned | Version name and timestamp are visible and properly positioned |
| 6 | Verify the row does not overflow or cause horizontal scrolling | Row fits within dropdown width; no overflow |
| 7 | Compare with other versions to ensure consistent layout | All version rows have consistent height and alignment |

## Expected Final State

Long creator name/email displays without breaking layout; text wraps or truncates; other metadata remains visible and aligned.

## Pass/Fail Criteria

**Pass:** Long creator info does not break layout; wraps or truncates gracefully; other metadata visible and aligned; no overflow

**Fail:** Layout breaks; text overflows; metadata hidden or misaligned; horizontal scrolling required
