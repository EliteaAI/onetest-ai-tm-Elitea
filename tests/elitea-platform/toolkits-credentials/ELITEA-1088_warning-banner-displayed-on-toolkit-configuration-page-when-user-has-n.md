---
id: ELITEA-1088
title: "Warning banner displayed on Toolkit Configuration page when user has no matching private credential"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1088: Warning banner displayed on Toolkit Configuration page when user has no matching private credential

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a styled warning banner replaces the old plain red error text when a team member opens a shared toolkit that references a private credential they do not have.

**Coverage:**
- AC1: Redesigned error banner shown below Credentials dropdown
- Correct banner text format with bold prefix and hyperlink
- Absence of raw FormHelperText / raw backend error string

## Preconditions

- Logged in as **User B** (non-author team member, no private credential matching the toolkit's required ID)
- Team Project exists with a toolkit (e.g., Jira type) configured to use a private credential with ID `team_jira_cred` belonging to User A
- Browser: Chrome (latest)

## Test Data

- Team project name: any team project
- Toolkit name: e.g., `Jira Team Toolkit`
- Required credential ID: `team_jira_cred`
- Credential type: Jira

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and navigate to the Team Project. | Team Project dashboard is displayed. |
| 2 | Navigate to the Toolkits section in the sidebar. | Toolkits list is displayed. |
| 3 | Open the team toolkit (e.g., `Jira Team Toolkit`). | Toolkit detail view opens. |
| 4 | Go to the Configuration tab. | Configuration form is visible. |
| 5 | Observe the area below the Credentials dropdown. | A styled warning banner is shown — NOT a plain red FormHelperText. |
| 6 | Read the banner text carefully. | Banner reads: **"Credential setup required:"** `This toolkit requires your own private Jira credentials.` `Create a credential` `with the ID "team_jira_cred" in your Private workspace to use this toolkit.` |
| 7 | Verify **"Credential setup required:"** is visually bold. | The prefix "Credential setup required:" is rendered in bold font weight. |
| 8 | Verify **"Create a credential"** is a clickable hyperlink. | "Create a credential" is underlined and styled in an accent/link color. |
| 9 | Search the entire page for the string `Value error` or `Configuration with title`. | No raw backend error string of the form `Value error, Configuration with title '...' not found for project_id ...` is visible anywhere on the page. |
| 10 | Verify no plain red FormHelperText error message is visible below the Credentials dropdown. | Old-style plain red error text is absent. |

## Expected Final State

Old-style plain red error text is absent.

## Pass/Fail Criteria

**Pass:**
- Styled warning banner is visible below the Credentials dropdown
- Banner text, bold label, and hyperlink all match the specification exactly
- No raw backend error or old FormHelperText is present

**Fail:**
- Banner is absent
- Plain red FormHelperText appears instead of the new banner
- Raw backend error string is visible on the page
- Banner text is incorrect (wrong type name, wrong ID, missing hyperlink)
