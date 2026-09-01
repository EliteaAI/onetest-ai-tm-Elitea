---
id: ELITEA-3023
title: "Admin Configuration Page — Previously Stored Config Remains Fully Usable After a Blocked Save"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3023: Admin Configuration Page — Previously Stored Config Remains Fully Usable After a Blocked Save

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a save is rejected due to malformed YAML (per `admin#37`'s new validation checkpoint), nothing is written — the config on disk/in storage is untouched, the pylon keeps running on it, and any credential in the old config continues to authenticate correctly. This is the core regression guarantee the fix depends on (validation only ever blocks a write; it never touches existing storage).

---

## Preconditions

- A pylon with a valid, working config (including a working credential/password) is currently running.
- Access to Admin → Configuration for that pylon.

---

## Test Data

| Field | Value |
|-------|-------|
| Malformed edit (any of) | `password: fo: bar` (unquoted colon+space) — reuse case from ELITEA-3020 |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Confirm the pylon is currently running and the existing credential works (e.g. the associated toolkit/plugin can authenticate). | Baseline confirmed working. |
| 2 | Open the raw YAML editor, introduce the malformed password edit, and attempt to Save. | Save is rejected (per ELITEA-3020). |
| 3 | Without reloading, close the editor / navigate away without saving again. | No further action taken. |
| 4 | Reopen the Configuration page for the same pylon. | Config shown is the original valid config, not the rejected edit. |
| 5 | Confirm the pylon is still running (no crash triggered by the attempted save). | Pylon unaffected — the rejected save never reached persistence or restart. |
| 6 | Re-test the original credential (e.g. re-authenticate the associated toolkit/plugin). | Still works exactly as before — unaffected by the blocked save attempt. |

---

## Expected Final State

The blocked save has zero effect on the pylon's running state or stored config; the original credential continues to function.

---

## Pass/Fail Criteria

**Pass:** Pylon keeps running, stored config is unchanged, original credential still authenticates after the blocked save attempt.
**Fail:** Pylon crashes or restarts as a side effect of the attempted save, stored config is partially overwritten, or the original credential stops working.
