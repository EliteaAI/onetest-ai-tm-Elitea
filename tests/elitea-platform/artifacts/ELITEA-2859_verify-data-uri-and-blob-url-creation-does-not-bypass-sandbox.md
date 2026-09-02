---
id: ELITEA-2859
title: "Verify data: URI and blob: URL creation in inline JS does not bypass sandbox"
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
| File | `data-uri-attempt.html` — attempts `window.open('data:text/html,...')` and `URL.createObjectURL(...)` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `data-uri-attempt.html` and open in Preview mode | Page loads |
| 2 | Observe whether a new tab/window opens | No new tab/window opens |
| 3 | Open DevTools → Console | Attempt is blocked or logs a SecurityError |

## Expected Final State

`data:`/`blob:` URL tricks cannot be used to escape the sandbox or open new windows.

## Pass/Fail Criteria

**Pass:**
- No popup/window opens; Console shows a block or SecurityError

**Fail:**
- A new tab/window opens with attacker-controlled content
