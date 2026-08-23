---
id: ELITEA-1977
title: "Credential — Create Project Credential from Toolkit Flow"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_create_project_from_toolkit_dropdown.TestCredentialCreateProjectFromToolkitDropdown.test_create_project_credential_from_toolkit_dropdown
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1704
---

# ELITEA-1977: Credential — Create Project Credential from Toolkit Flow

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can create a project-scoped credential directly from a toolkit's credential dropdown, and that the credential is visible to all project members after being linked to the toolkit.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with an existing toolkit that uses Github credentials.
- The Credentials and Toolkits sections are accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit type | Github-based toolkit |
| Project credential name | autotest_project_cred |
| Token value | (any valid or placeholder token) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Toolkits section from the sidebar | Toolkits list page loads |
| 2 | Open an existing Github toolkit | Toolkit detail/configuration page loads |
| 3 | In the toolkit Configuration section, click the credential dropdown (e.g., "Github Configuration *") | Dropdown opens showing CREATE and "Saved github Credentials" sections |
| 4 | Under the CREATE section, click "New project github credentials" (briefcase icon) | Credential creation form opens with Github type pre-selected |
| 5 | Fill in Display Name: "autotest_project_cred" and Token value | Fields accept the input |
| 6 | Save the credential | Credential is saved successfully |
| 7 | Navigate back to the toolkit | Toolkit configuration page loads |
| 8 | Click the credential dropdown again | Dropdown reopens |
| 9 | Click the "Refresh the configurations" button | List refreshes |
| 10 | Verify "autotest_project_cred" appears in the saved credentials list | Newly created credential is visible |
| 11 | Select "autotest_project_cred" | Credential is linked to the toolkit |
| 12 | Verify this credential is visible to all project members (project scope) | Credential is accessible to all members of the project |

---

## Expected Final State

"autotest_project_cred" is created as a project-scoped credential, linked to the toolkit, and visible to all project members.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Project credential is created, appears in the toolkit dropdown after refresh, is linked successfully, and has project-level visibility.

**Fail:**
- Any step produces an error or unexpected result.
- Project credential is not created, does not appear in the dropdown, or is not visible to other project members.
