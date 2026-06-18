---
id: ELITEA-1098
title: "Warning banner appears in Pipeline configuration when attached toolkit has a private credential mismatch"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, r-2.0.2, 4416]
requirements: [EliteaAI/elitea_issues#4416]
---
# ELITEA-1098: Warning banner appears in Pipeline configuration when attached toolkit has a private credential mismatch

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the styled warning banner is shown in the Pipeline Configuration when a toolkit with a private credential mismatch is attached, and the Pipeline page loads without errors.

**Coverage:**
- AC5: Consistent banner in Pipeline configuration
- Absence of raw backend error in Pipeline UI
- Pipeline configuration page integrity

## Preconditions

- Logged in as **User B** (no matching private credential)
- A Team Project Pipeline exists with the mismatched-credential toolkit attached

## Test Data

- Pipeline name: any pipeline in the team project using the mismatched toolkit
- Required credential ID: `team_jira_cred`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B and navigate to the Team Project → Pipelines. | Pipelines list is displayed. |
| 2 | Open the Pipeline that has the mismatched-credential toolkit attached. | Pipeline detail view opens. |
| 3 | Navigate to the toolkit configuration section within the Pipeline. | Toolkit configuration section is visible. |
| 4 | Locate the mismatched toolkit entry. | Toolkit entry is displayed. |
| 5 | Observe the area below or adjacent to the mismatched toolkit. | A styled warning banner is shown (same style as on the Toolkit and Agent configuration pages). |
| 6 | Read the banner text. | Banner content includes the correct credential type and required ID. |
| 7 | Check the page for raw backend error strings. | No raw backend error string is visible. |
| 8 | Verify the Pipeline configuration page loads fully with no broken sections. | All sections render correctly. |

## Expected Final State

All sections render correctly.

## Pass/Fail Criteria

**Pass:**
- Styled warning banner is visible in Pipeline configuration for the mismatched toolkit
- No raw backend error string is present
- Pipeline configuration page loads completely

**Fail:**
- Banner is absent in the Pipeline configuration
- Raw backend error is displayed
- Page has broken/empty sections
