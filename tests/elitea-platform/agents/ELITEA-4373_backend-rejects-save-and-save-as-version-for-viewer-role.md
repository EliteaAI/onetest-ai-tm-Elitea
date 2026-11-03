---
id: ELITEA-4373
title: "Backend Rejects Direct Save and Save As Version API Calls for Viewer Role on Agent Details (access_denied, No Persistence)"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#7302]
---

## Preconditions

- A user account with the **Viewer** role in a project containing at least one existing Agent (e.g. `Special Testing` project)
- A separate Editor or Admin session available to capture a baseline and verify no change persisted
- Browser DevTools (Network tab, "Copy as fetch") or an equivalent API client capable of replaying an authenticated request

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Role | Viewer |
| Project | `Special Testing` (or any project where the test account has Viewer role) |
| Agent | Any existing agent, e.g. `Confluence Cloud Toolkit` |
| Save endpoint | Application update endpoint, requires `models.applications.application.update` |
| Save As Version endpoint | Application save-as-version endpoint, requires `models.applications.application.update` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Editor/Admin, open the test Agent and note its current instructions text and version list (baseline). | Baseline state recorded. |
| 2 | Log in as the Viewer-role user and open the Agent Details page for the same Agent. Open DevTools → Network tab. | Page loads in read-only context; Network tab is ready to capture requests. |
| 3 | Make a local edit (e.g. modify the instructions text) and trigger the Save action in the UI to capture the exact outgoing request (method, URL, headers including auth token, body). Use "Copy as fetch" or equivalent. | The Save request is captured with full headers and payload. |
| 4 | Replay the captured Save request directly (DevTools console `fetch(...)`, Postman, or curl) using the Viewer's own credentials. | Response is an authorization error: `{"ok": false, "error": "access_denied", ..., "required": ["models.applications.application.update"]}`. No 2xx success status is returned. |
| 5 | Repeat steps 3–4 for the Save As Version endpoint, using the Viewer's credentials. | Same `access_denied` response with `required: ["models.applications.application.update"]` is returned; no new version is created. |
| 6 | As Editor/Admin, reload the Agent Details page and compare the Agent's instructions text and version list against the baseline from step 1. | State is unchanged — no new version appears, no field was modified by either of the Viewer's direct API attempts. |

## Expected Final State

The Agent's persisted configuration and version list are identical to the pre-test baseline; both direct API attempts made by the Viewer were rejected server-side with `access_denied` and produced no side effects.

## Pass/Fail Criteria

**Pass:**
- The direct Save API call as Viewer returns `access_denied` with `required: ["models.applications.application.update"]` and no 2xx status
- The direct Save As Version API call as Viewer returns the same denial
- No new version is created and no field is persisted as a result of either call

**Fail:**
- Either endpoint returns a success status (2xx) for the Viewer-issued request
- Any change (new version, modified instructions/field) is visible after reload, indicating the Viewer's call was partially or fully persisted
