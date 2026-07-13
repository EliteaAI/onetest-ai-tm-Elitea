---
id: ELITEA-1966
title: "Filter Credentials by Type"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1966: Filter Credentials by Type

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the type filter in the credentials list sidebar correctly filters credentials to show only those matching the selected type, and that removing the filter restores the full list.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and credentials of different types exist (e.g., Github, Jira, Confluence).

---

## Test Data

| Field | Value |
|-------|-------|
| Credential types | Github, Jira, Confluence |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure credentials of different types exist (Github, Jira, Confluence) | Credentials list shows mixed types |
| 2 | Navigate to the credentials list | Credentials list page loads |
| 3 | Click the "Github" type filter in the right sidebar | Only Github-type credentials are displayed |
| 4 | Click the "Jira" type filter (removing Github filter first) | Only Jira-type credentials are displayed |
| 5 | Remove the active type filter | All credential types are shown again |

---

## Expected Final State

The type filter narrows the displayed credentials to the selected type; removing the filter restores the full credential list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each type filter correctly limits the displayed credentials to the matching type.

**Fail:**
- Any step produces an error or unexpected result.
- Filtering shows incorrect credentials or does not respond to type selection.
