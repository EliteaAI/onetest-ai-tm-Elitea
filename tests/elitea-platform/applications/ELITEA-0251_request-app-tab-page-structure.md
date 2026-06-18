---
id: ELITEA-0251
title: "Request App Tab: Page Structure"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0251: Request App Tab: Page Structure

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Applications page loads correctly with the right heading, subtitle, and default active tab.

**Coverage:**
- Sidebar "Applications" item navigates to the page
- "Request App" is the default active tab
- Page heading and subtitle render correctly

## Preconditions

- Logged in as a project member
- At least one project exists
- Navigate to {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click 'Applications' in the left sidebar | Applications page loads; 'Request App' tab is active by default |
| 2 | Observe the page heading | 'Request an application' is displayed |
| 3 | Observe the subtitle text | 'Choose a ready application to configure for this project, or request access when it is not yet available.' is displayed |

## Expected Final State

'Choose a ready application to configure for this project, or request access when it is not yet available.' is displayed

## Pass/Fail Criteria

**Pass:**
- Sidebar navigation works
- Request App tab is active by default
- Heading and subtitle match expected text exactly

**Fail:**
- Tab is not default
- Heading or subtitle is missing or incorrect
