---
id: ELITEA-3041
title: "Renaming a Header to a Case-Insensitive Duplicate of an Existing Header Is Silently Blocked by the UI Guard"
priority: medium
type: ui-validation
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3041: Renaming a Header to a Case-Insensitive Duplicate of an Existing Header Is Silently Blocked by the UI Guard

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Medium · **Type:** UI Validation

**Objective:** Confirm, per `SecretHeadersInput.jsx`'s `handleNameChange`, that attempting to rename a header to a name that is a case-insensitive duplicate of another existing header's name is silently no-op'd by the UI — the rename does not take effect, and no two rows end up with case-insensitively-identical names. This is a client-side guard, not a save-time validation error.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.
- At least 2 header rows already added, one named `X-Trace-Id`.

---

## Test Data

| Field | Value |
|-------|-------|
| Existing header | `X-Trace-Id` |
| Attempted rename (on the other row) | `x-trace-id` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Add two header rows; name the first `X-Trace-Id`. | Row 1 accepts the name. |
| 2 | Attempt to rename the second row to `x-trace-id` (same name, different casing). | The rename is silently blocked — the second row's name field does **not** change to `x-trace-id`; it retains its previous value. |
| 3 | Confirm no error toast/message is shown for this specific interaction (per code, this is a silent no-op, not an explicit validation error). | Document whether any feedback is shown; per the component's code, none is expected. |
| 4 | Confirm the two rows still have distinct names (not case-insensitively identical). | No duplicate names exist among the rows. |

---

## Expected Final State

Case-insensitively duplicate header names can never coexist in the form state, enforced silently at rename time.

---

## Pass/Fail Criteria

**Pass:** The duplicate rename attempt is blocked; the row keeps its prior name; no two rows end up with case-insensitively identical names.
**Fail:** The rename succeeds, producing two rows with case-insensitively identical names (e.g. `X-Trace-Id` and `x-trace-id` coexisting).
