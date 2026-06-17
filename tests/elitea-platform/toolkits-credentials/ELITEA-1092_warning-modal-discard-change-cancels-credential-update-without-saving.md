---
id: ELITEA-1092
title: "Warning modal \"Discard change\" cancels credential update without saving"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1092: Warning modal "Discard change" cancels credential update without saving

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "Discard change" in the credential warning modal closes it and reverts the credential dropdown to its original value without persisting any change.

**Coverage:**
- AC6: Discard action in the warning modal
- Credential value reverted on discard
- Change not persisted after page reload

## Preconditions

- Logged in as any team member (User A or User B) with edit access to the team project toolkit
- Team toolkit has an existing credential assigned

## Test Data

- Original credential: `team_jira_cred` (currently saved on the toolkit)
- Alternative credential: any other credential selectable from the dropdown

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Team Project → Toolkits and open the toolkit. | Toolkit configuration opens. |
| 2 | Note the current value of the Credentials dropdown (e.g., `team_jira_cred`). | Current credential is displayed. |
| 3 | Change the Credentials dropdown to a different value. | Dropdown shows the new selection. |
| 4 | Click Save. | The "Credential Configuration Change" warning modal appears. |
| 5 | Click **"Discard change"**. | Modal closes immediately. |
| 6 | Observe the Credentials dropdown value on the form. | Dropdown reverts to the **original credential** (`team_jira_cred`). |
| 7 | Reload the page. | Toolkit configuration reloads showing the original credential — no change was saved. |

## Expected Final State

Toolkit configuration reloads showing the original credential — no change was saved.

## Pass/Fail Criteria

**Pass:**
- Modal closes after "Discard change"
- Credentials dropdown reverts to original value
- No change is persisted after reload

**Fail:**
- Modal does not close on "Discard change"
- Changed credential remains in the dropdown after discard
- Changed credential is persisted to the server despite discarding
