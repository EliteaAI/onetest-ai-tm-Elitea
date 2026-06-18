---
id: ELITEA-1091
title: "\"Create a credential\" hyperlink opens pre-filled credential creation in a new tab"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1091: "Create a credential" hyperlink opens pre-filled credential creation in a new tab

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the "Create a credential" link in the warning banner opens the credential creation page in a new browser tab with credential type, Display Name, and Credential ID pre-filled from the toolkit context.

**Coverage:**
- AC2: Hyperlink opens pre-filled credential creation
- New tab behaviour (original tab unchanged)
- Pre-filled type, Display Name, and Credential ID
- Credential created under user's Private workspace

## Preconditions

- Logged in as **User B** with the warning banner visible on the team toolkit configuration page
- Toolkit type: Jira, required credential ID: `team_jira_cred`

## Test Data

- Expected pre-filled Display Name: `team_jira_cred`
- Expected pre-filled Credential ID: `team_jira_cred`
- Expected pre-selected type: Jira

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, open the team toolkit configuration — the warning banner is visible. | Banner with "Create a credential" hyperlink is shown. |
| 2 | Click the **"Create a credential"** hyperlink in the banner. | A new browser tab opens. The original tab remains open and unchanged. |
| 3 | Observe the URL of the new tab. | The new tab URL points to the credential creation page within User B's **Private workspace** (private project scope). |
| 4 | Verify the **credential type** selector on the creation form. | The type is pre-selected as **Jira** (matching the toolkit type). |
| 5 | Verify the **Display Name** field value. | Display Name is pre-filled with `team_jira_cred`. |
| 6 | Verify the **Credential ID** field value. | Credential ID is pre-filled with `team_jira_cred`. |
| 7 | Verify which fields remain empty. | Only secret fields (API key, token, password, username) are empty and require manual entry. |
| 8 | Return to the original toolkit tab. | Original tab is still open showing the same toolkit configuration with the banner. |

## Expected Final State

Original tab is still open showing the same toolkit configuration with the banner.

## Pass/Fail Criteria

**Pass:**
- New tab opens with the credential creation form
- Credential type, Display Name, and ID are all correctly pre-filled
- New tab is scoped to User B's Private workspace
- Original tab is unaffected

**Fail:**
- Link does not open a new tab (opens in same tab or no navigation occurs)
- Credential type, Display Name, or ID is not pre-filled or is incorrect
- New tab opens in a team project instead of Private workspace
