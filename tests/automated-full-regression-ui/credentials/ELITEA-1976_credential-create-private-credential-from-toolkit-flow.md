---
id: ELITEA-1976
title: "Toolkit Credential Creation — Private & Project"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1976: Toolkit Credential Creation — Private & Project

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that users can create both private and project-scoped credentials directly from a toolkit's credential dropdown, and that each credential type has the correct visibility scope (private to creator only, project visible to all members).

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
| Private credential name | autotest_private_cred |
| Project credential name | autotest_project_cred |
| Token value | (any valid or placeholder token) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **PRIVATE CREDENTIAL Phase** | | |
| 1 | Navigate to the Toolkits section from the sidebar | Toolkits list page loads |
| 2 | Open an existing Github toolkit | Toolkit detail/configuration page loads |
| 3 | In the toolkit Configuration section, click the credential dropdown (e.g., "Github Configuration *") | Dropdown opens showing CREATE and "Saved github Credentials" sections |
| 4 | Verify the dropdown shows two sections: "CREATE" and "Saved github Credentials" | Both sections are visible |
| 5 | Verify the CREATE section has two options: "New private github credentials" (person icon) and "New project github credentials" (briefcase icon) | Both options are present with correct icons |
| 6 | Click "New private github credentials" | Credential creation form opens with Github type pre-selected |
| 7 | Fill in Display Name: "autotest_private_cred" and Token value | Fields accept the input |
| 8 | Save the credential | Credential is saved successfully |
| 9 | Navigate back to the toolkit | Toolkit configuration page loads |
| 10 | Click the credential dropdown again | Dropdown reopens |
| 11 | Click the "Refresh the configurations" button next to "Saved github Credentials" header | List refreshes |
| 12 | Verify "autotest_private_cred" appears in the saved credentials list | Newly created credential is visible |
| 13 | Select "autotest_private_cred" | Credential is linked to the toolkit |
| 14 | Verify this credential is only visible to the creator (private scope) | Credential is not visible to other project members |
| **PROJECT CREDENTIAL Phase** | | |
| 15 | Click the credential dropdown again | Dropdown opens |
| 16 | Under the CREATE section, click "New project github credentials" (briefcase icon) | Credential creation form opens with Github type pre-selected |
| 17 | Fill in Display Name: "autotest_project_cred" and Token value | Fields accept the input |
| 18 | Save the credential | Credential is saved successfully |
| 19 | Navigate back to the toolkit | Toolkit configuration page loads |
| 20 | Click the credential dropdown again | Dropdown reopens |
| 21 | Click the "Refresh the configurations" button | List refreshes |
| 22 | Verify "autotest_project_cred" appears in the saved credentials list | Newly created credential is visible |
| 23 | Select "autotest_project_cred" | Credential is linked to the toolkit |
| 24 | Verify this credential is visible to all project members (project scope) | Credential is accessible to all members of the project |

---

## Expected Final State

Both private and project credentials are successfully created from the toolkit dropdown, each with the correct visibility scope: private credential visible only to its creator, project credential visible to all project members.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both credential creation options are present with correct icons; private credential has private scope; project credential has project-level visibility; both appear in the toolkit dropdown after refresh and can be linked successfully.

**Fail:**
- Any step produces an error or unexpected result.
- CREATE section options are missing or incorrect; private credential is visible to other members; project credential is not visible to all members; credentials do not appear in the dropdown or cannot be linked.

---

## Notes

**Source functional tests:** ELITEA-1976 (Create Private Credential from Toolkit), ELITEA-1977 (Create Project Credential from Toolkit)

**Regression rationale:** Consolidates both private and project credential creation flows from the toolkit dropdown into one comprehensive scenario. Both flows share the same starting context (toolkit credential dropdown) and validation steps (CREATE section presence, icon verification, refresh mechanism, linking success), making them natural candidates for consolidation while preserving distinct scope validation.

**Selected checkpoints:** CREATE section shows both options with correct icons (person for private, briefcase for project); credential creation forms open with pre-selected type; both credentials save successfully; refresh button makes new credentials appear in dropdown; credentials can be selected and linked; private credential has private scope (creator only); project credential has project scope (all members).
