---
id: ELITEA-3020
title: "Admin Configuration Page — Save Is Blocked for Unquoted Colon+Space Password in Raw YAML"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3020: Admin Configuration Page — Save Is Blocked for Unquoted Colon+Space Password in Raw YAML

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Admin → Configuration page's raw YAML editor does not allow saving a pylon/plugin config whose password value is unquoted and contains a colon followed by a space — the exact corruption scenario named in issue #6268 — now that `admin#37` added a `yaml.safe_load()` validation checkpoint to the `action=="save"` POST handler (`api/v2/runtime_pylons_config.py`) before this reaches storage.

---

## Preconditions

- Logged in as an ELITEA admin user with access to Admin → Configuration.
- At least one pylon/plugin config exists and currently loads successfully (a known-good baseline to compare against after the test).

---

## Test Data

| Field | Value |
|-------|-------|
| Raw YAML edit | `password: fo: bar` (i.e. an unquoted scalar value that itself contains `: `) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Admin → Configuration, open the raw YAML editor for the target pylon/plugin config. | Editor loads showing the current valid config. |
| 2 | Edit the `password` line to the unquoted value `fo: bar` (i.e. `password: fo: bar`), leaving the rest of the config untouched. | Editor shows the edited text; no client-side error yet (unless client-side validation exists). |
| 3 | Click Save. | Save is **not** silently accepted. Either a client-side validation error appears before any request is sent, or the request is sent and the backend's `400` response (`{"error": "Invalid YAML: <exc>"}`) is surfaced to the admin as a legible on-screen error — not a silent no-op, not a raw console error, not a generic content-free toast. |
| 4 | Open the browser Network tab and inspect the save request's response. | Response status is `400` (not `500`, not `200`). Response body contains the PyYAML exception text, no stack trace, no internal file path. |
| 5 | Reload the Configuration page and reopen the same config. | The editor shows the **previous, valid** config exactly as it was before step 2 — not the corrupted text, not a blank/broken state. |

---

## Expected Final State

The malformed save attempt is rejected with a legible error; the previously-stored valid config is untouched and still loads correctly.

---

## Pass/Fail Criteria

**Pass:** Save is blocked, a clear error is shown to the admin, network response is `400`, and the config on reload is unchanged from before the attempt.
**Fail:** Save appears to succeed (success toast, no error) while the backend actually rejected it; OR the corrupted text persists into the stored config; OR the error shown is a raw stack trace/generic failure with no actionable detail.
