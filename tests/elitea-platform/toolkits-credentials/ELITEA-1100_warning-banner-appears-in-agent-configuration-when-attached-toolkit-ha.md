---
id: ELITEA-1100
title: "Warning banner appears in Agent configuration when attached toolkit has a private credential mismatch"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1100: Warning banner appears in Agent configuration when attached toolkit has a private credential mismatch

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the same styled warning banner shown on the Toolkit page is also shown in the Agent Configuration when a toolkit with a private credential mismatch is attached, and no raw backend error is displayed.

**Coverage:**
- AC4: Consistent banner in Agent configuration
- Absence of raw backend error string in Agent UI
- Agent configuration page loads without broken sections

## Preconditions

- Logged in as **User B** (no matching private credential)
- A Team Project Agent exists with the mismatched-credential toolkit attached

## Test Data

- Agent name: any agent in the team project using the mismatched toolkit
- Required credential ID: `team_jira_cred`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and navigate to the Team Project → Agents. | Agents list is displayed. |
| 2 | Open the Agent that has the mismatched-credential toolkit attached. | Agent detail view opens. |
| 3 | Navigate to the Configuration tab or the Toolkits panel within the agent. | Toolkit list or configuration section is visible. |
| 4 | Locate the row or section for the mismatched toolkit. | Toolkit entry is visible in the agent configuration. |
| 5 | Observe the area below or adjacent to the mismatched toolkit. | A styled warning banner is shown (same style as on the Toolkit Configuration page). |
| 6 | Read the banner text. | Banner content includes the credential type and required ID, formatted consistently with AC1. |
| 7 | Check the page for raw backend error strings (`Value error`, `Configuration with title`). | No raw backend error string is visible anywhere on the Agent configuration page. |
| 8 | Verify the Agent configuration page loads fully with no broken sections or empty panels. | All sections render correctly; no blank/broken UI elements. |

## Expected Final State

All sections render correctly; no blank/broken UI elements.

## Pass/Fail Criteria

**Pass:**
- Styled warning banner is visible in the Agent configuration for the mismatched toolkit
- No raw backend error string is present
- Page loads fully without broken sections

**Fail:**
- Banner is absent in the Agent configuration
- Raw backend error string is displayed
- Agent configuration page has broken/empty sections
