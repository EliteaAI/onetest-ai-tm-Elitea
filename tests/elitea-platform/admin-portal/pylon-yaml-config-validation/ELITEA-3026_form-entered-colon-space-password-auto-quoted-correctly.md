---
id: ELITEA-3026
title: "Password With Colon+Space Entered Through the Login Form Field Is Serialized as Valid, Quoted YAML"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, new]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3026: Password With Colon+Space Entered Through the Login Form Field Is Serialized as Valid, Quoted YAML

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** [[ELITEA-3024]] and [[ELITEA-3025]] confirm the backend checkpoint doesn't over-reject *already-quoted* input. This test covers the more realistic real-world trigger for issue #6268: a user typing a password with reserved characters into a normal form field (not hand-editing raw YAML). Confirm whatever code path serializes that form input into YAML quotes it correctly on the way in, so the save doesn't get needlessly rejected by the new validation checkpoint due to the serializer's own bug (as opposed to the user's input).

---

## Preconditions

- Logged in as an ELITEA admin user (or, if the credential is set via a client-facing Login Form flow, as that end-user role) with access to the credential/password entry field feeding into pylon/plugin config.
- Access to view the resulting raw YAML afterward (Admin → Configuration) to confirm serialization.

---

## Test Data

| Field | Value |
|-------|-------|
| Password typed into the form field | `fo: bar` (colon + space, entered as plain text — not hand-quoted by the user) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Locate the credential/password entry point that feeds into this pylon/plugin's YAML config (e.g. the Login Form credential field, or the Configuration page's structured password field if one exists separate from the raw YAML editor). | Field is available and accepts free-text input. |
| 2 | Type `fo: bar` into the password field and submit/save through the normal (non-raw-YAML) UI flow. | Save completes without the admin needing to manually add quotes. |
| 3 | Inspect the resulting raw YAML (Admin → Configuration raw editor, or an equivalent read path) for this config. | The `password` value is written as a **properly quoted** scalar (e.g. `password: "fo: bar"` or `password: 'fo: bar'`) — not as an unquoted `password: fo: bar`, which would be invalid YAML and would have been rejected by the new checkpoint. |
| 4 | Confirm the save actually succeeded end-to-end (no 400, no error toast). | Save succeeded — proving the serializer correctly escaped the value rather than the admin having to intervene. |
| 5 | If applicable, verify the credential authenticates using the literal value `fo: bar`. | Authentication succeeds. |

---

## Expected Final State

A colon+space password entered through the normal form flow is auto-quoted into valid YAML by the serializer, and the save is not blocked.

---

## Pass/Fail Criteria

**Pass:** The form-entered password is serialized as properly-quoted YAML and the save succeeds without the user needing to manually quote it.
**Fail:** The serializer writes an unquoted value, causing the save to be rejected by the new validation checkpoint for input the user never hand-edited — i.e. the fix (validation) exposes a pre-existing serialization gap as a hard failure where before #6268 it silently corrupted storage. Either way this is a gap worth filing: the fix should not make a normal form-based password entry fail.
