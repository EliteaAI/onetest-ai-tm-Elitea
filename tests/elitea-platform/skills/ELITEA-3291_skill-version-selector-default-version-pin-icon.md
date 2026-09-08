---
id: ELITEA-3291
title: "Default version pin icon displays and functions correctly in Skills"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with a default version set exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Test Skill | Skill with default version configured |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a Skill with a default version set | Skill loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Locate the default version in the list | Default version row visible |
| 4 | Verify an active/filled pin icon is displayed next to the default version | Pin icon visible and filled/active |
| 5 | Hover over the pin icon | Tooltip appears |
| 6 | Verify the tooltip displays "Default version" | Tooltip text is correct |
| 7 | Verify the default version indicator is independent of selection indicator | Pin icon present regardless of whether version is selected |
| 8 | Select a different (non-default) version | Version switches |
| 9 | Reopen the dropdown | Dropdown opens |
| 10 | Verify default version still shows pin icon even though not selected | Pin icon persists on default version |
| 11 | Select the default version | Default version now selected |
| 12 | Verify both checkmark and pin icon are displayed | Both indicators visible simultaneously |

## Expected Final State

Default version displays an active pin icon with correct tooltip. Pin icon is independent of selection state—a version can be default and selected, or default but not selected.

## Pass/Fail Criteria

**Pass:**
- Pin icon visible on default version
- Tooltip displays "Default version"
- Pin icon persists regardless of selection state
- Both pin and checkmark can coexist on same version

**Fail:**
- Pin icon missing on default version
- Incorrect or missing tooltip
- Pin icon disappears when version not selected
- Pin icon conflicts with checkmark display
