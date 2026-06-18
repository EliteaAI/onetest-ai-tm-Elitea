---
id: ELITEA-1095
title: "Banner does not appear for users with matching private credential of the same type and ID"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1095: Banner does not appear for users with matching private credential of the same type and ID

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the warning banner is correctly suppressed for a user who already has a private credential with both the matching type and the matching ID — the toolkit should display normally without the banner.

**Coverage:**
- Negative banner scenario — correct credential exists (same type AND same ID)
- Credentials dropdown shows expected value
- Form is fully interactive

## Preconditions

- Logged in as **User A** who has a private credential with ID `team_jira_cred` of type **Jira** — matching the team toolkit configuration exactly

## Test Data

- User A's private credential: ID=`team_jira_cred`, Type=Jira
- Team toolkit required credential: ID=`team_jira_cred`, Type=Jira

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A and navigate to the Team Project → Toolkits. | Toolkits list is displayed. |
| 2 | Open the team toolkit that requires credential ID `team_jira_cred` of type Jira. | Toolkit configuration opens. |
| 3 | Go to the Configuration tab. | Configuration form is visible. |
| 4 | Observe the area below the Credentials dropdown. | **No warning banner** is shown. The form is clean. |
| 5 | Verify the Credentials dropdown displays `team_jira_cred`. | Correct credential is pre-selected in the dropdown. |
| 6 | Verify the configuration form is fully interactive (not read-only). | All fields are editable; form is not locked. |

## Expected Final State

All fields are editable; form is not locked.

## Pass/Fail Criteria

**Pass:**
- No warning banner is shown
- Correct credential is displayed in the dropdown
- Form is fully interactive

**Fail:**
- Warning banner is shown for a user who has the correct matching credential
- Credentials dropdown is empty or shows wrong value
- Form is in read-only state despite correct credential being present
