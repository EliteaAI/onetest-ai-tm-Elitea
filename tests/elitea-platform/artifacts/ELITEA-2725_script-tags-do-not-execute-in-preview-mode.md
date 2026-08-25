---
id: ELITEA-2725
title: "Script tags do not execute in Preview mode - Security"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4, nfr:security]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file containing JavaScript is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | HTML file with script alert XSS Test /script |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate HTML with script tags containing alert | Test file is ready |
| 2 | Open the file in Preview mode | File opens in Canvas |
| 3 | Observe browser behavior | No alert popup appears |
| 4 | Check browser console (F12) | No script execution errors |
| 5 | Verify HTML/CSS renders | Static content displays |
| 6 | Switch to Raw mode | Script tags visible in source |

## Expected Final State

- No JavaScript alert appears
- Scripts are blocked/disabled in Preview iframe
- No security warnings to user
- Page renders HTML/CSS only
- Static content is displayed correctly

## Pass/Fail Criteria

**Pass:**
- No JavaScript alert appears
- Scripts are blocked in Preview
- No security warnings
- HTML/CSS renders correctly

**Fail:**
- JavaScript alert appears (XSS vulnerability)
- Scripts execute in Preview
- Security warnings appear
- Page behavior is affected by scripts

**Security Note:** This validates the sandbox requirement from the issue
