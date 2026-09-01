---
id: ELITEA-3022
title: "Admin Configuration Page — Save Is Blocked for Unescaped Single Quote Inside a Single-Quoted Password"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3022: Admin Configuration Page — Save Is Blocked for Unescaped Single Quote Inside a Single-Quoted Password

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Verify the raw YAML editor's save path blocks a config where the password is a single-quoted scalar containing an inner single quote that is not doubled (`''`) — malformed YAML per YAML 1.1 single-quote escaping rules, and should now be rejected before persistence.

---

## Preconditions

- Logged in as an ELITEA admin user with access to Admin → Configuration.
- A known-good baseline config exists for the target pylon/plugin.

---

## Test Data

| Field | Value |
|-------|-------|
| Raw YAML edit | `password: 'abc'def'` (single quote inside a single-quoted scalar, not escaped as `''`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the raw YAML editor for the target config. | Editor loads the current valid config. |
| 2 | Edit the `password` line to `password: 'abc'def'`. | Editor shows the edited text. |
| 3 | Click Save. | Save is rejected — either client-side, or via the backend's `400 {"error": "Invalid YAML: <exc>"}` surfaced legibly to the admin. |
| 4 | Check the Network tab response. | `400` status, PyYAML exception text only. |
| 5 | Reload and reopen the config. | Previous valid config is intact and unchanged. |

---

## Expected Final State

The malformed save attempt is rejected with a legible error; stored config remains the last valid version.

---

## Pass/Fail Criteria

**Pass:** Save blocked with a clear, actionable error; stored config unaffected.
**Fail:** Save silently succeeds, corrupts the stored config, or the error shown is unhelpful/absent.
