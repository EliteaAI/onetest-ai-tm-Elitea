---
id: ELITEA-2843
title: "Verify ELITEA session data is not accessible from the preview iframe"
priority: critical
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An artifact bucket exists and is available for file upload
- Browser DevTools available to inspect Console output

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `session-access-targeted.html` — probes `document.cookie`, `localStorage` (keys such as `elitea_mcp_tokens_v1`, `elitea_ui.project.id`, `elitea_ui.project_permission`, `ActiveConversationParticipantKey`), and `window.parent` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `session-access-targeted.html` to a bucket | File uploads successfully |
| 2 | Open the file in Preview mode | Probe page renders results for each check |
| 3 | Review the "Cookies" probe result | Shows "PASS: document.cookie is empty" |
| 4 | Review the "localStorage" probe result | Shows "PASS: localStorage blocked with SecurityError" OR "PASS: localStorage accessible but empty (0 keys)" — any listed key name is a FAIL |
| 5 | Review the "Parent frame" probe result | Shows "PASS: parent frame blocked with SecurityError" |
| 6 | Open DevTools → Console | `SecurityError` is logged for the `window.parent` and `localStorage` probes |

## Expected Final State

No ELITEA session data (tokens, user ID, project identifiers) is exposed to or readable from the sandboxed preview iframe.

## Pass/Fail Criteria

**Pass:**
- All three probes (cookies, localStorage, parent frame) report PASS with no real data exposed

**Fail:**
- Any probe returns actual ELITEA session/user/project data instead of empty/blocked
