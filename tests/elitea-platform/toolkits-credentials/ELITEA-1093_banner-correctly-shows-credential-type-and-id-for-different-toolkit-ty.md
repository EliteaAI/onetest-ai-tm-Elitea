---
id: ELITEA-1093
title: "Banner correctly shows credential type and ID for different toolkit types"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1093: Banner correctly shows credential type and ID for different toolkit types

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the warning banner dynamically uses the correct credential type name and the exact required credential ID for at least two different toolkit types.

**Coverage:**
- Dynamic banner content per toolkit type
- Correct type label (Jira, GitHub, etc.) in banner text
- Correct credential ID in banner text

## Preconditions

- Logged in as **User B** (no matching private credentials for either toolkit)
- Two team project toolkits exist: one **Jira** type (required ID: `team_jira_cred`) and one **GitHub** type (required ID: `team_github_cred`)

## Test Data

| Toolkit | Type | Required Credential ID |
|---|---|---|
| Jira Team Toolkit | Jira | `team_jira_cred` |
| GitHub Team Toolkit | GitHub | `team_github_cred` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and navigate to the Team Project → Toolkits. | Toolkits list is displayed. |
| 2 | Open the **Jira Team Toolkit** → Configuration tab. | Configuration form and warning banner are shown. |
| 3 | Read the banner text. | Banner reads: *"...private **Jira** credentials..."* and shows ID `team_jira_cred`. |
| 4 | Navigate back and open the **GitHub Team Toolkit** → Configuration tab. | Configuration form and warning banner are shown. |
| 5 | Read the banner text. | Banner reads: *"...private **GitHub** credentials..."* and shows ID `team_github_cred`. |
| 6 | Verify there is no mismatch between the banner type label and the actual toolkit type for either toolkit. | Type label in banner matches the toolkit type exactly in both cases. |

## Expected Final State

Type label in banner matches the toolkit type exactly in both cases.

## Pass/Fail Criteria

**Pass:**
- Jira banner shows "Jira" as type and `team_jira_cred` as ID
- GitHub banner shows "GitHub" as type and `team_github_cred` as ID
- No cross-contamination of type or ID between banners

**Fail:**
- Banner shows incorrect type name for either toolkit
- Banner shows incorrect credential ID
- Same banner text appears regardless of toolkit type
