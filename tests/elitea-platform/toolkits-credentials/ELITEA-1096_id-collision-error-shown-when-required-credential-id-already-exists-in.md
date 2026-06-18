---
id: ELITEA-1096
title: "ID collision error shown when required credential ID already exists in Private workspace"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1096: ID collision error shown when required credential ID already exists in Private workspace

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a user clicks "Create a credential" from the banner and attempts to save a credential whose ID already exists in their Private workspace, the standard ID collision error is displayed and no duplicate is created.

**Coverage:**
- AC8: Pre-filled ID collision handling
- Duplicate credential not created
- User can take corrective action (edit ID or cancel)

## Preconditions

- Logged in as **User B**
- User B already has a credential with ID `team_jira_cred` in their Private workspace (of any type)
- The team toolkit warning banner is visible with required ID `team_jira_cred`

## Test Data

- Required credential ID: `team_jira_cred`
- User B's existing credential: ID=`team_jira_cred` (any type)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, open the team toolkit configuration — warning banner is visible. | Banner is shown with "Create a credential" link. |
| 2 | Click **"Create a credential"** in the banner. | New tab opens with credential creation form, ID pre-filled as `team_jira_cred`. |
| 3 | Fill in the required secret fields. | Secrets are entered. |
| 4 | Click Save. | An ID collision error message is shown (e.g., "A credential with this ID already exists"). |
| 5 | Navigate to Private workspace → Credentials and verify no duplicate was created. | Only one credential with ID `team_jira_cred` exists. |
| 6 | Verify the error allows the user to modify the ID or cancel the action. | ID field becomes editable, or a cancel option is available. |

## Expected Final State

ID field becomes editable, or a cancel option is available.

## Pass/Fail Criteria

**Pass:**
- ID collision error is shown on save attempt
- No duplicate credential is created
- User can take corrective action

**Fail:**
- No error shown — duplicate credential created
- Form is submitted silently with a different ID
- Error shown but no way to correct the ID
