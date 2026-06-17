---
id: ELITEA-0025
title: "Information Card Displays Manually Configured Plugin Versions"
priority: high
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0025: Information Card Displays Manually Configured Plugin Versions

**Module:** Resources Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that the plugin versions field on the Information card accepts manual input, persists after save and page reload, and is displayed on the user-facing Resources page. ELITEA version and install/upgrade date auto-sourcing are not yet implemented and are out of scope. Partially covers AC5 of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.
Note: ELITEA version and install/upgrade date auto-sourcing from the environment are NOT yet implemented — those fields require manual configuration and are out of scope for this test. This test covers only plugin versions.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources and open the Information card section. | Information card configuration is visible. |
| 2 | Check the plugin versions field and enter or verify a plugin version value. | Plugin version field is present and accepts input. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Reload the Configuration → Resources page and check the Information card. | The saved plugin version value persists. |
| 5 | Open the user-facing Resources page and view the Information card. | The configured plugin version is displayed to users on the Resources page. |

## Expected Final State

The configured plugin version is displayed to users on the Resources page.

## Pass/Fail Criteria

Pass: Plugin versions field is present, accepts input, persists after save, and is displayed on the Resources page.
Fail: Field is missing, does not save, or does not appear on the Resources page.
Out of scope (not yet implemented): ELITEA version and install/upgrade date auto-sourcing from the environment.
