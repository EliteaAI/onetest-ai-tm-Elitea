---
id: ELITEA-2348
title: "Viewer and Monitor roles cannot access Secrets section"
priority: medium
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_viewer_role_cannot_access_secrets.TestViewerRoleCannotAccessSecrets.test_viewer_role_is_not_offered_the_secrets_section
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1912"
---

# ELITEA-2348: Viewer and Monitor roles cannot access Secrets section

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Viewer and Monitor roles cannot access Secrets section. Success is confirmed when verify monitor role is also blocked from accessing secrets.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as a user with Viewer role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 3 | Verify the section is either not visible in the sidebar OR shows an "Access Denied" error | Condition holds as described. |
| 4 | Log out and log in as a user with Monitor role | Action completes without error and produces the expected UI state. |
| 5 | Repeat steps 2–3 | Action completes without error and produces the expected UI state. |
| 6 | Verify Monitor role is also blocked from accessing Secrets | Condition holds as described. |

---

## Expected Final State

Verify Monitor role is also blocked from accessing Secrets.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Viewer and Monitor roles cannot access Secrets section.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
