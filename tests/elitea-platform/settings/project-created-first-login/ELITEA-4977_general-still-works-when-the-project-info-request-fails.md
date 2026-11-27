---
id: ELITEA-4977
title: "General still works when the project info request fails"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** If the project-info request fails, General renders without Project created and without errors.

## Preconditions

- User is logged in to `{{base_url}}`
- A way to fail the request: DevTools → Network → **Block request URL** for `*project-info*`, or a proxy answering HTTP 500

## Test Data

| Field | Value |
|-------|-------|
| Request | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Fail the project-info request and open Settings → **General** | The page opens; the other General sections render |
| 2 | Look at the project header | No Project created item, no "Invalid Date", no fallback date |
| 3 | Check the browser console | No uncaught errors |
| 4 | Remove the block and reload | Project created is shown again |

## Expected Final State

A failing project-info call does not break Settings → General.

## Pass/Fail Criteria

**Pass:**
- General is usable; Project created is simply absent

**Fail:**
- Blank or broken page, error screen, "Invalid Date" or an invented date
