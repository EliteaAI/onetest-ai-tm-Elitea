---
id: ELITEA-3027
title: "POST Pylon Config (action=save) With Malformed YAML Returns 400 and Persists Nothing"
priority: high
type: functional
module: pylon-yaml-config-validation
status: draft
execution_type: manual
tags: [admin, credentials, yaml-validation, issue:6268, api]
requirements: [EliteaAI/elitea_issues#6268]
---

# ELITEA-3027: POST Pylon Config (action=save) With Malformed YAML Returns 400 and Persists Nothing

**Module:** Admin Portal / Pylon YAML Config Validation · **Priority:** High · **Type:** Functional

**Objective:** Direct API-level confirmation of the checkpoint added in `admin#37` to `api/v2/runtime_pylons_config.py`: a `POST` with `action=="save"` and malformed YAML in `data` must return `400` with `{"error": "Invalid YAML: <exc>"}`, must **not** fire the `bootstrap_runtime_update` event, and must not persist the malformed text — confirmed independently of the Admin UI, covering any caller (script, integration, future UI) that hits this endpoint directly.

---

## Preconditions

- Valid Keycloak/admin-service credentials with permission to call the pylon config endpoint directly (`api/v2/runtime_pylons_config.py`).
- A known target `pylon_id` with an existing valid config.
- HTTP client (curl/Postman/API test tool) capable of sending an authenticated POST.

---

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `POST` to the pylon config resource, `{pylon_id}` |
| Body | `{"action": "save", "data": "password: fo: bar\n"}` (malformed: unquoted colon+space inside the raw YAML text) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Send the POST with the malformed `data` payload above and `action: "save"`. | Response status is `400`. |
| 2 | Inspect the response body. | Body is `{"error": "Invalid YAML: <exc>"}` where `<exc>` is the PyYAML parser's exception text — no stack trace, no internal file path. |
| 3 | Check server logs (if accessible) for this request. | A `log.warning()` entry is present, including the `pylon_id`, for audit/incident-analysis purposes. |
| 4 | Immediately GET the current config for the same `pylon_id`. | Config returned is the previous valid config — unchanged by the rejected POST. |
| 5 | Confirm (via logs, monitoring, or an event-observing mechanism if available) that no `bootstrap_runtime_update` event was fired for this rejected request. | No event fired — the pylon is never told to reload/restart with the rejected data. |

---

## Expected Final State

The malformed POST is rejected with a clean `400`, no persistence occurs, and no runtime-update event fires.

---

## Pass/Fail Criteria

**Pass:** `400` returned with a clean error message; config unchanged on immediate re-read; no runtime-update event fired.
**Fail:** Request returns `200`/`{"ok": true}` despite malformed input; OR returns a `500`/raw traceback instead of a clean `400`; OR the config is partially/fully overwritten with the malformed text.
