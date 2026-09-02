---
id: ELITEA-2864
title: "Verify postMessage from iframe cannot trigger ELITEA parent window actions"
priority: medium
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
| File | `postmessage-test.html` — calls `window.parent.postMessage('elitea-exfil-test', '*')` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `postmessage-test.html` and open in Preview mode | Script runs on load |
| 2 | Open DevTools → Console | No ELITEA listener responds to the message |
| 3 | Observe ELITEA UI state | Unchanged after the message is sent |

## Expected Final State

The ELITEA parent application does not act on messages posted from the sandboxed preview iframe.

## Pass/Fail Criteria

**Pass:**
- No ELITEA response or state change occurs

**Fail:**
- ELITEA UI reacts to the posted message in any observable way
