---
id: ELITEA-4379
title: "Version Dropdown Remains Visible and Read-Only Functional for Viewer on Agent Details"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role, with access to an Agent that has more than one saved version
- Viewer is logged in and has the Agent Details page open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Agent | An existing agent with at least 2 versions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer-role user and open the test Agent's Details page. | Page loads; the version-selector dropdown is visible in the header/toolbar. |
| 2 | Click to open the version dropdown. | Dropdown opens and lists all available versions with their metadata (name/creator/timestamp), same as for Editor/Admin. |
| 3 | Select a different version from the dropdown. | The page switches to display that version's content in read-only mode; no error occurs. |
| 4 | Confirm Save, Save As Version, and Discard remain hidden after switching versions. | The three controls are still hidden for the Viewer regardless of which version is being viewed. |
| 5 | Close the dropdown by clicking outside it. | Dropdown closes normally. |

## Expected Final State

The version dropdown on Agent Details remains fully visible and functional in read-only mode for the Viewer, unaffected by the Save/Save As Version/Discard visibility fix.

## Pass/Fail Criteria

**Pass:**
- Version dropdown is visible, opens, lists all versions, and allows read-only version switching for Viewer
- Save/Save As Version/Discard remain hidden across all versions viewed

**Fail:**
- Version dropdown is hidden, broken, or fails to list/switch versions for Viewer as a side effect of this fix
- Any of Save/Save As Version/Discard becomes visible when viewing a specific version as Viewer
