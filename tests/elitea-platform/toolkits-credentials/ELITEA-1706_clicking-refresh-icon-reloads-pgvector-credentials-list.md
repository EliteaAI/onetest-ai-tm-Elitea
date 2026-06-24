---
id: ELITEA-1706
title: Verify clicking refresh icon reloads PGVector credentials list
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:pgvector, feat:toolkits, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5356]
---
# ELITEA-1706: Verify clicking refresh icon reloads PGVector credentials list

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the refresh icon to the right of "SAVED PGVECTOR CREDENTIALS" heading successfully reloads the credentials list with latest data without closing the dropdown.


## Preconditions

- User is logged in to `{{base_url}}`
- At least one PGVector credential exists
- User has access to agent configuration

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to agent configuration page | Page loads |
| 2 | Expand "Toolkit" section | Section expands |
| 3 | Click on "Pgvector Configuration" dropdown | Dropdown opens |
| 4 | Note the current number of credentials displayed | Credential count is noted |
| 5 | Click the refresh icon (to the right of "SAVED PGVECTOR CREDENTIALS" heading) | Loading indicator appears briefly if applicable; credentials list refreshes; dropdown remains open |
| 6 | (Optional) In another tab/window, create a new PGVector credential via Settings | New credential is created |
| 7 | Return to agent configuration, open PGVector dropdown | Dropdown opens |
| 8 | Click refresh icon | New credential appears in the list after refresh |

## Expected Final State

Refresh icon successfully reloads the credentials list with latest data without closing the dropdown.

## Pass/Fail Criteria

**Pass:**
- Clicking refresh icon triggers credential reload
- Loading indicator appears briefly if applicable
- Credentials list updates with latest data
- Dropdown remains open after refresh
- New credentials appear after refresh
- Deleted credentials disappear after refresh
- No JavaScript errors in console

**Fail:**
- Refresh icon doesn't work
- Credentials list doesn't update
- Dropdown closes on refresh
- JavaScript errors occur
