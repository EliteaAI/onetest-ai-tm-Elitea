---
id: ELITEA-4961
title: "Missing First login or Project created shows no error and no fallback date"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** When the timestamps are missing, the UI degrades gracefully: First login shows `—`, Project created is hidden.

## Preconditions

- User is logged in to `{{base_url}}`
- Chrome DevTools is open (Network → right-click a request → **Override content**) to simulate missing values; no environment data has null values

## Test Data

| Field | Value |
|-------|-------|
| First login source | `GET {{base_url}}/api/v2/social/author/` (fills the user state; overriding `auth/user/default` has no effect) |
| Override 1 | `social/author/` response with `"first_login": null` |
| Override 2 | `project-info` response with `"created_at": null` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Apply override 1 and open Settings → **Profile** | First login shows `—`; Last login still shows its real value; First login is still directly above Last login |
| 2 | Remove override 1, apply override 2, open Settings → **General** | The header shows the project name and Teammates; **Project created is not shown** (by design in EliteaUI#1548 — the issue's AC-6 says `—`); no fallback date |
| 3 | Remove the override and select the **Public** project | Project created is not shown for the Public project (by design in EliteaUI#1548) |
| 4 | Check the browser console | No uncaught errors; no "Invalid Date", "NaN" or "Something went wrong" |

## Expected Final State

Missing values never produce an error, a crash or an invented date.

## Pass/Fail Criteria

**Pass:**
- First login `—`, Project created hidden, no errors

**Fail:**
- Any error, "Invalid Date", or a substituted date (now, Last login)
