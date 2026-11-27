---
id: ELITEA-4999
title: "Team project Editor and Viewer can't see or call Delete Project Data"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

# ELITEA-4999: Team project Editor and Viewer can't see or call Delete Project Data

**Module:** settings-users-and-roles · **Priority:** critical · **Type:** functional

**Objective:** Admin-only Delete Project Data stays closed to team Editors and Viewers, in the UI and in the API.

---

## Preconditions

- User A (Admin of team project T) and User B are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of T

---

## Test Data

| B's role in T | Delete Project Data section | Delete probe (GET / POST) |
|---|---|---|
| Editor | Hidden | 403 / 403 `access_denied` |
| Viewer | Hidden | 403 / 403 `access_denied` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, add User B to T with the role from the Test Data row | `GET admin/users/default/{T id}` shows B with only that role |
| 2 | As User B, open Settings → General of T | General settings open; the **Delete Project Data** section is not shown |
| 3 | As User B, run the delete probe on T | GET and POST both return 403 `access_denied` |
| 4 | Repeat steps 1–3 for the next row (User A changes B's role) | Same result |
| 5 | As User A, remove User B from T | B is no longer a member |

---

## Expected Final State

Neither role could see or call Delete Project Data; B is not a member of T.

---

## Pass/Fail Criteria

**Pass:**
- Section hidden and both probe calls 403 for Editor and for Viewer

**Fail:**
- The section is shown to either role, or any probe call returns 200/400

---

## Notes

- **Source functional tests:** ELITEA-4985 (`tests/elitea-platform/settings/private-project-owner-admin/`)
- **Regression rationale:** The negative side of the role matrix: an admin-only feature must not open to Editors or Viewers in the UI or the API.
- **Selectors (`data-testid`):** `project-general-section`, `project-data-delete-section` (expected count 0)
- Run User B in a second browser context with B's own session; User A changes B's role with the REST calls in the test data README.
- Assert "section absent" only after `project-general-section` is visible and the project-info query has settled, or the check passes too early.
- B gets its own "What's New" modal on first load: dismiss it ("Got it" or `button[aria-label="close"]`) before screenshots.
- Remove B from T in a `finally` block so a failed run doesn't leave B as a member.
