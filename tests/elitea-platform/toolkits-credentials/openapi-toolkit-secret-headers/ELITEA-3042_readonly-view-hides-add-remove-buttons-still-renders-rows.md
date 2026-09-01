---
id: ELITEA-3042
title: "Read-Only/Disabled Credential View Hides Add and Remove Header Buttons but Still Renders Existing Rows"
priority: low
type: ui-validation
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, feat:credentials, int:openapi, issue:6002, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3042: Read-Only/Disabled Credential View Hides Add and Remove Header Buttons but Still Renders Existing Rows

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** Low · **Type:** UI Validation

**Objective:** Confirm, per `SecretHeadersInput.jsx`'s `disabled` prop handling, that in a read-only/disabled credential view (e.g. viewing a shared or non-owned credential), the "+ Add header" button and per-row remove buttons are hidden, while existing header rows still render (view-only, not editable).

---

## Preconditions

- Logged in to `{{base_url}}`.
- An OpenAPI credential with at least one additional header configured, viewable in a read-only/disabled context (e.g. a shared credential viewed without edit permission, if reachable in the UI).

---

## Test Data

| Field | Value |
|-------|-------|
| Existing header | `X-Api-Key: (masked)` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the credential in its read-only/disabled view. | The "Additional Secret Headers" section is visible. |
| 2 | Inspect the existing header row(s). | Row(s) render showing the name (and masked value), same as in edit mode. |
| 3 | Look for the "+ Add header" button. | Button is hidden/not rendered. |
| 4 | Look for the remove button on the existing row. | Remove button is hidden/not rendered for that row. |

---

## Expected Final State

The section is fully visible in read-only mode but offers no way to add or remove headers.

---

## Pass/Fail Criteria

**Pass:** Existing rows render; Add and Remove buttons are both hidden in the read-only/disabled view.
**Fail:** Add or Remove buttons are still shown (allowing edits in a supposedly read-only view), or existing rows fail to render at all.
