---
id: ELITEA-0958
title: "Page Header Version String Visibility in Both Themes"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0958: Page Header Version String Visibility in Both Themes

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ELITEA version string in the Resources page header is correctly formatted and clearly visible in both Light Mode and Dark Mode.

**Coverage:**
- Version string format: Version: X.X.X (DD-Mon-YYYY)
- (i) info icon visible next to version string
- Version string readability in both Light and Dark themes
- Version string matches actual installed environment version

## Preconditions

Logged in to ELITEA; on the Resources page
Known installed version of the environment (e.g., 2.0.2 (30-Apr-2026))

## Test Data

Expected version string format: Version: X.X.X (DD-Mon-YYYY)
Example: Version: 2.0.2 (30-Apr-2026)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page in Light Mode. | Resources page loads. |
| 2 | Locate the version string in the top-right area of the header. | Version string is visible. |
| 3 | Confirm the version string format matches: Version: X.X.X (DD-Mon-YYYY) — e.g., Version: 2.0.2 (30-Apr-2026). | Format is correct with version number and date in parentheses. |
| 4 | Confirm an (i) info icon is visible next to the version string. | (i) icon is present and visible in Light Mode. |
| 5 | Confirm the version number matches the known installed version of the environment. | Version number matches the actual environment version. |
| 6 | Switch to Dark Mode. | Theme switches to Dark Mode. |
| 7 | Confirm the version string is still clearly visible against the dark header background. | Version string is legible in Dark Mode (no invisible white-on-white or dark-on-dark text). |
| 8 | Confirm the (i) icon is still visible in Dark Mode. | (i) icon is present and visible in Dark Mode. |

## Expected Final State

(i) icon is present and visible in Dark Mode.

## Pass/Fail Criteria

**Pass:**
- Version string visible in the header in both themes
- Format matches Version: X.X.X (DD-Mon-YYYY) exactly
- (i) icon visible next to the version string in both themes
- Version string matches the actual installed version

**Fail:**
- Version string is absent or hidden in either theme
- Version string format does not match expected pattern
- (i) icon is absent
- Version string shows incorrect or placeholder version number
