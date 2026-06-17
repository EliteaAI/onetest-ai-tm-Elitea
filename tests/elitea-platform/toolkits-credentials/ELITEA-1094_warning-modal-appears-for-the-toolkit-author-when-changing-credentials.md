---
id: ELITEA-1094
title: "Warning modal appears for the toolkit author when changing credentials on a Team Project toolkit"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1094: Warning modal appears for the toolkit author when changing credentials on a Team Project toolkit

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Credential Configuration Change" warning modal also appears for the toolkit **author** (not only non-authors) when saving a credential change on a team project toolkit.

**Coverage:**
- AC6: Warning modal for any user including the author
- Complementary to non-author scenario (Bug #4649)

## Preconditions

- Logged in as **User A** (the toolkit author/creator)
- Team project toolkit exists with a credential configured

## Test Data

- Toolkit: any team project toolkit created by User A
- Alternative credential: any other credential selectable from the dropdown

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User A and navigate to the Team Project → Toolkits. | Toolkits list is displayed. |
| 2 | Open the team toolkit authored by User A. | Toolkit configuration opens. |
| 3 | Go to the Configuration tab. | Configuration form is visible. |
| 4 | Change the Credentials dropdown to a different available credential. | Dropdown selection changes. |
| 5 | Click Save. | The **"Credential Configuration Change"** warning modal appears. |
| 6 | Verify modal title and body text match specification. | Title is "Credential Configuration Change"; body warns about team impact. |
| 7 | Click **"Confirm change"**. | Modal closes. Change is saved successfully without error. |
| 8 | Reload the toolkit configuration. | Updated credential is shown in the dropdown. |

## Expected Final State

Updated credential is shown in the dropdown.

## Pass/Fail Criteria

**Pass:**
- Modal appears for User A (the author)
- Confirm saves successfully
- Change persists after reload

**Fail:**
- Modal does not appear for the author
- Save bypasses the modal for the author
