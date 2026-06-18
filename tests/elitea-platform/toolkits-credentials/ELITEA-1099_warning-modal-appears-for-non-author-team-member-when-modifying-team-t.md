---
id: ELITEA-1099
title: "Warning modal appears for non-author team member when modifying team toolkit credentials"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1099: Warning modal appears for non-author team member when modifying team toolkit credentials

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Credential Configuration Change" confirmation modal is triggered for any team member (including non-authors) who changes the credential configuration of a team project toolkit — regression coverage for Bug EliteaAI/elitea_issues#4649.

**Coverage:**
- AC6: Warning modal shown on Team Toolkit credential change
- Non-author user scenario (Bug EliteaAI/elitea_issues#4649 regression)
- Modal content, buttons, and successful save after confirmation

## Preconditions

- User A has created a team toolkit with a private credential assigned
- **User B** (non-author) has edit access to the same team project
- User B is logged in
- Browser: Chrome (latest)

## Test Data

- Team toolkit: any team project toolkit with credentials configured
- Alternative credential: any other available credential User B can select from the dropdown

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and navigate to the Team Project. | Team Project dashboard is displayed. |
| 2 | Navigate to Toolkits and open the team toolkit created by User A. | Toolkit configuration opens. |
| 3 | Go to the Configuration tab. | Configuration form is visible. |
| 4 | Change the Credentials dropdown to a different available credential. | Dropdown selection changes. |
| 5 | Click Save. | A modal dialog titled **"Credential Configuration Change"** appears with a warning icon. |
| 6 | Read the modal body text. | Body reads: *"Changing the credential may make this toolkit non-operational for other team members who do not have a matching Private credential. Make this decision considering the potential impact on your team."* |
| 7 | Verify two buttons are visible in the modal. | Buttons **"Discard change"** and **"Confirm change"** (red button) are visible. |
| 8 | Click **"Confirm change"**. | Modal closes. Save operation completes successfully. No error toast or 500 error is shown. |
| 9 | Reload the toolkit configuration page. | The newly selected credential is reflected in the Credentials dropdown. |

## Expected Final State

The newly selected credential is reflected in the Credentials dropdown.

## Pass/Fail Criteria

**Pass:**
- Modal appears for the non-author user immediately after clicking Save
- Modal title, body text, and both buttons match specification
- "Confirm change" saves successfully with no error
- Change persists after page reload

**Fail:**
- Modal does not appear for non-author user
- Internal server error (500) is shown after clicking "Confirm change"
- Credential change is not persisted after confirmation
- Modal appears but has incorrect title, body, or button labels
