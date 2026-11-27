---
id: ELITEA-4997
title: "Private project owner holds Admin and can open Delete Project Data"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

# ELITEA-4997: Private project owner holds Admin and can open Delete Project Data

**Module:** settings-users-and-roles · **Priority:** critical · **Type:** functional

**Objective:** The owner of a private project holds the project Admin role (with Editor and Viewer), so the admin-only Delete Project Data feature is available to them.

---

## Preconditions

- User A is logged in to `{{base_url}}` and owns private project P-A. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- P-A has at least one agent
- DevTools → Network is open to watch for `POST .../admin/project_data_delete/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Page | `{{base_url}}/app/{P-A id}/settings/project-general` |
| Roles API | `GET {{base_url}}/api/v2/admin/users/default/{P-A id}` |
| Delete probe | `GET` and `POST {"types": []}` on `{{base_url}}/api/v2/admin/project_data_delete/prompt_lib/{P-A id}` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call the roles API for P-A | User A's row has the roles `admin`, `editor` and `viewer` |
| 2 | Open Settings → General of P-A | The page opens and the **Delete Project Data** section is shown |
| 3 | In Delete Project Data, select **Agents** | **Delete selected data** becomes enabled |
| 4 | Click **Delete selected data** | The confirmation modal opens; **Delete** is disabled until the confirmation phrase is typed |
| 5 | Click **Cancel** | The modal closes. The network log has no `POST .../project_data_delete/...` |
| 6 | Run the delete probe (GET, then POST with `{"types": []}`) | GET 200 with the summary; POST 400 "types must be a non-empty list" (authorized, nothing deleted) |

---

## Expected Final State

User A is Admin of P-A, the Delete Project Data feature is available to them, and no project data was deleted.

---

## Pass/Fail Criteria

**Pass:**
- User A holds `admin`, `editor`, `viewer` in P-A
- The section is shown, the modal opens and Delete is gated by the phrase
- Probe: GET 200 / POST 400

**Fail:**
- User A lacks `admin` in P-A
- The section is hidden, or the probe returns 403
- Any delete request is sent

---

## Notes

- **Source functional tests:** ELITEA-4983 (`tests/elitea-platform/settings/private-project-owner-admin/`)
- **Regression rationale:** The core #7507 outcome: a private owner is a project Admin and reaches an admin-only feature.
- **Selectors (`data-testid`):** `project-general-section`, `project-data-delete-section`, `project-data-type-agents`, `project-data-delete-open`, `project-data-delete-modal`, `project-data-delete-confirm`, `project-data-delete-cancel`
- Use the API as the oracle for roles and the probe; run the probe in User A's own session (`page.request` or `fetch` with the session cookies).
- Watch requests matching `POST /project_data_delete/` from the moment the modal opens and fail on any hit. Never click Delete: this is a shared project.
- The section is rendered only after the project-info query settles: wait for `project-general-section` before asserting that `project-data-delete-section` is present.
- A burst of probe calls can get a Cloudflare 429 HTML page; back off and retry, it isn't a product answer.
- The full dialog gating (Select all, wrong-case phrase) is covered by ELITEA-4656.
