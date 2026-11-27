---
id: ELITEA-4982
title: "Missing First login or Project created shows no error and no made-up date"
priority: critical
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

# ELITEA-4982: Missing First login or Project created shows no error and no made-up date

**Objective:** When the timestamps are missing, the UI degrades gracefully: First login shows `—` and Project created is hidden.

## Preconditions

- User is logged in to `{{base_url}}`
- Chrome DevTools is open (Network → right-click a request → **Override content**) to simulate missing values; no environment data has null values

## Test Data

| Field | Value |
|-------|-------|
| First login source | `GET {{base_url}}/api/v2/social/author/` (fills the user state; overriding `auth/user/default` has no effect) |
| Override 1 | `social/author/` response with `"first_login": null` |
| Override 2 | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` response with `"created_at": null` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Apply override 1 and open Settings → **Profile** | First login shows `—`; Last login still shows its real value; First login is still directly above Last login |
| 2 | Remove override 1, apply override 2 and open Settings → **General** | The header shows the project name and Teammates; **Project created is not shown** (by design in EliteaUI#1548); no fallback date |
| 3 | Remove override 2 and select the **Public** project | Project created is not shown for the Public project (by design in EliteaUI#1548) |
| 4 | Check the page and the browser console | No uncaught errors; no "Invalid Date", "NaN" or "Something went wrong" |

## Expected Final State

Missing values never produce an error, a crash or an invented date.

## Pass/Fail Criteria

**Pass:**
- First login shows `—`, Project created is hidden, and there are no errors

**Fail:**
- Any error, "Invalid Date", or a substituted date (now, Last login)

## Notes

- **Source functional tests:** ELITEA-4970 (`tests/elitea-platform/settings/project-created-first-login/`)
- **Regression rationale:** The AC-6 failure mode: missing values must not break Settings or show a wrong date. 1:1 with the source case.
- **Selected checkpoints:** First login `—`; Last login unaffected; Project created hidden for `created_at: null` and for Public; no errors.
- **Automation:** intercept the responses (e.g. Playwright `page.route` + `route.fetch()`, then patch the JSON) instead of DevTools overrides. Mock `social/author/`, **not** `auth/user/default`: the user state is filled from `social/author/`. Assert that the mock fired, and remove each route before the next step.
- The issue's AC-6 says "missing values display `—`". The PR hides Project created instead; it shows `—` only for First login. If the product changes to `—` for Project created, update step 2.
- Do not use malformed (non-null) values here: they render "Invalid Date" through the shared date formatter. That case was dropped from scope on 2026-11-27.
