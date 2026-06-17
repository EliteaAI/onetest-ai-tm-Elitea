---
id: ELITEA-1090
title: "Refresh button in credential dropdown loads newly created credential and resolves the banner"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1090: Refresh button in credential dropdown loads newly created credential and resolves the banner

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that after creating the matching private credential in a new tab, clicking the Refresh button in the Credentials dropdown loads the new credential and selecting it hides the warning banner.

**Coverage:**
- AC3: Refresh loads newly created credential
- Banner dismissed after selecting matching credential
- Credential persisted after Save

## Preconditions

- Logged in as **User B**
- Warning banner is visible on the team toolkit configuration page
- Required credential ID: `team_jira_cred`

## Test Data

- New credential to create: type=Jira, Display Name=`team_jira_cred`, Credential ID=`team_jira_cred`, with valid API key/token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, open the team toolkit configuration — the warning banner is visible. | Banner is shown. |
| 2 | Click **"Create a credential"** in the banner to open the new tab. | Credential creation form opens pre-filled. |
| 3 | Fill in the required secret fields (API key, username, etc.) and click Save. | New credential `team_jira_cred` of type Jira is saved in User B's Private workspace. |
| 4 | Return to the original toolkit configuration tab. | Original tab still shows the banner. |
| 5 | Click the **Refresh (🔄) icon** inside the **Credentials** dropdown. | Dropdown list refreshes. |
| 6 | Observe the Credentials dropdown list. | The newly created credential `team_jira_cred` appears in the list. |
| 7 | Select the newly created credential `team_jira_cred` from the dropdown. | Credential is selected. The warning banner **disappears** from the form. |
| 8 | Click Save. Confirmation modal appears (team project). Click **"Confirm change"**. | Save completes successfully. |
| 9 | Reload the toolkit configuration page. | The credential `team_jira_cred` is displayed; no warning banner is shown. |

## Expected Final State

The credential `team_jira_cred` is displayed; no warning banner is shown.

## Pass/Fail Criteria

**Pass:**
- New credential appears in the dropdown after Refresh
- Banner disappears upon selecting the matching credential
- Credential is saved and banner remains absent after reload

**Fail:**
- Refresh does not load the new credential
- Banner persists after selecting the matching credential
- Banner reappears after save and reload
