---
id: ELITEA-3025
title: "Password Containing Colon+Space Wrapped in Single Quotes Saves Successfully and Round-Trips Exactly"
priority: medium
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, new]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3025: Password Containing Colon+Space Wrapped in Single Quotes Saves Successfully and Round-Trips Exactly

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** Medium · **Type:** Functional

**Objective:** Same over-rejection check as [[ELITEA-3024]], but for single-quoted scalars — confirm the validation checkpoint accepts a colon+space password when wrapped in single quotes (equally valid YAML), not just double quotes.

---

## Preconditions

- Logged in as an ELITEA admin user with access to Admin → Configuration.
- A pylon/plugin config exists to edit.

---

## Test Data

| Field | Value |
|-------|-------|
| Raw YAML edit | `password: 'fo: bar'` (literal password value is `fo: bar`, properly single-quoted) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the raw YAML editor for the target config. | Editor loads the current valid config. |
| 2 | Edit the `password` line to `password: 'fo: bar'`. | Editor shows the edited text. |
| 3 | Click Save. | Save succeeds — no error, `{"ok": True}` / 200 response. |
| 4 | Reload and reopen the config. | Value round-trips to the exact literal string `fo: bar`. |

---

## Expected Final State

The single-quoted colon+space password saves without error and round-trips exactly.

---

## Pass/Fail Criteria

**Pass:** Save succeeds; value round-trips exactly to `fo: bar`.
**Fail:** Save is incorrectly rejected, or the value is altered/truncated on save or reload.
