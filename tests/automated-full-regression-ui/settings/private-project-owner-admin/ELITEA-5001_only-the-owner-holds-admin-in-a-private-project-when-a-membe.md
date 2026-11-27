---
id: ELITEA-5001
title: "Only the owner holds Admin in a private project when a member is added or promoted"
priority: critical
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:roles-permissions, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7507]
---

# ELITEA-5001: Only the owner holds Admin in a private project when a member is added or promoted

**Module:** settings-users-and-roles · **Priority:** critical · **Type:** functional

**Objective:** The owner-only Admin guard strips `admin` for anyone but the owner of a private project, both when a member is added and when their roles are changed.

---

## Preconditions

- User A (owner of P-A) and User B are available. Accounts and API calls: [test-data/private-project-owner-admin](../../../../test-data/private-project-owner-admin/README.md)
- User B is not a member of P-A. Note the "Teammates: N" count on P-A's Settings → General

---

## Test Data

| Field | Value |
|-------|-------|
| Add | `POST {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"emails": ["<B email>"], "roles": ["admin", "editor"]}` |
| Promote | `PUT {{base_url}}/api/v2/admin/users/default/{P-A id}` `{"id": <B id>, "roles": ["admin"]}` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, send the Add request | B becomes a member of P-A with `editor` and without `admin` (`GET admin/users/default/{P-A id}`) |
| 2 | As User A, send the Promote request | B still has no `admin`; User A still holds `admin` |
| 3 | Reload P-A's Settings → General | "Teammates" is one higher than before; User A still sees Delete Project Data |
| 4 | As User A, remove B from P-A | B is no longer a member |

---

## Expected Final State

User A is the only Admin of P-A; B is not a member.

---

## Pass/Fail Criteria

**Pass:**
- B never holds `admin` in P-A, after the add or the promote
- User A keeps `admin`

**Fail:**
- B holds `admin` at any point, or User A loses it

---

## Notes

- **Source functional tests:** ELITEA-4987 (`tests/elitea-platform/settings/private-project-owner-admin/`)
- **Regression rationale:** The owner-only Admin guard is the server-side safeguard of #7507; if it regresses, any owner could hand out Admin of a private project.
- **Selectors (`data-testid`):** `project-general-section` (its text holds "Teammates: N"), `project-data-delete-section`
- A private project has no Settings → Users page (it redirects to General), so membership is checked through REST and the Teammates count.
- Assert on the membership after each request, not on the response: both requests answer 200 even though `admin` was dropped. Record the response text; see also ELITEA-4990 and ELITEA-4995.
- Remove B from P-A in a `finally` block.
