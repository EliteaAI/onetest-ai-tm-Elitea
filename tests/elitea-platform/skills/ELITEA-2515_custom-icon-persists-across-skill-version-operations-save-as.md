---
id: ELITEA-2515
title: "Custom icon persists across skill version operations save as version"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- At least one Skill exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version Name | `v2` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or edit a Skill and assign a custom icon | Custom icon applied |
| 2 | Save the Skill | Save succeeds |
| 3 | Use "Save As Version" to create a new version (e.g., `v2`) | New version created |
| 4 | Verify the original `base` version retains the custom icon | Custom icon on base |
| 5 | Switch to the new `v2` version | Version switched |
| 6 | Verify the new `v2` version has the custom icon | Custom icon on v2 (or verify expected behavior per implementation) |

## Expected Final State

When using "Save As Version", the custom icon is preserved in both the original and new version.

## Pass/Fail Criteria

**Pass:**
- Original version retains custom icon
- New version has custom icon
- Version operations work correctly

**Fail:**
- Icon lost on version creation
- Icon differs between versions unexpectedly
- Version operation fails
