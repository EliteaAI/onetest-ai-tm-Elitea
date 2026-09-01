---
id: ELITEA-3024
title: "Password Containing Colon+Space Wrapped in Double Quotes Saves Successfully and Round-Trips Exactly"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, new]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3024: Password Containing Colon+Space Wrapped in Double Quotes Saves Successfully and Round-Trips Exactly

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Verify the new `yaml.safe_load()` validation checkpoint (added in `admin#37`, `api/v2/runtime_pylons_config.py` `action=="save"` branch) does **not over-reject** valid input: a password containing a colon followed by a space is syntactically valid YAML as long as it's properly double-quoted, and must save successfully with the literal value preserved exactly.

---

## Preconditions

- Logged in as an ELITEA admin user with access to Admin → Configuration.
- A pylon/plugin config exists to edit.

---

## Test Data

| Field | Value |
|-------|-------|
| Raw YAML edit | `password: "fo: bar"` (literal password value is `fo: bar`, properly double-quoted) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the raw YAML editor for the target config. | Editor loads the current valid config. |
| 2 | Edit the `password` line to `password: "fo: bar"`. | Editor shows the edited text. |
| 3 | Click Save. | Save **succeeds** — no error shown, `{"ok": True}` / 200 response, `bootstrap_runtime_update` event fires. This is valid YAML and must not be blocked by the validation checkpoint. |
| 4 | Reload the Configuration page and reopen the config. | The `password` field/line still reflects the value `fo: bar` — colon, space, and quoting intact (or at minimum round-trips to the identical literal string on any re-serialization). Not truncated at the colon, not split, not silently stripped of quotes in a way that would make a later save invalid. |
| 5 | If this credential is actually used to authenticate (e.g. backing a toolkit/plugin login), exercise that authentication. | Authentication succeeds using the literal value `fo: bar` exactly — confirming the value used at runtime matches what was saved, not a mangled version. |

---

## Expected Final State

The quoted colon+space password saves without error and is preserved exactly, both in storage and in actual use.

---

## Pass/Fail Criteria

**Pass:** Save succeeds with no error; password value round-trips to the exact literal string `fo: bar`; authentication (if applicable) succeeds using that literal value.
**Fail:** Save is incorrectly rejected as if it were malformed YAML (over-rejection bug); OR the value is corrupted/truncated/altered on save or reload; OR authentication fails despite the value appearing correct in the editor.
