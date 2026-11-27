---
id: ELITEA-4970
title: "Project info and user APIs return persisted timestamps in a stable format"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** The APIs behind the two fields return stable, persisted values and respect access rules and field filters.

## Preconditions

- An API token for **User A**; **User B** is not a member of User A's Private project
- Use `Authorization: Bearer <token>`

## Test Data

| Field | Value |
|-------|-------|
| Projects | User A Private, a team project, the Public project |
| Endpoints | `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info`, `GET {{base_url}}/api/v2/auth/user/default`, `GET {{base_url}}/api/v2/social/author/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call project-info twice for each project | `created_at` is ISO 8601 with UTC offset (e.g. `2026-05-18T09:51:50.852274+00:00`) and identical in both calls |
| 2 | Call project-info with `?fields=created_at`, then `?fields=teammates_count` | The first returns `created_at`; the second omits it |
| 3 | As User B, call project-info for User A's Private project | HTTP 403 (or 404) with no `created_at` |
| 4 | Call `auth/user/default` and `social/author/` | Both return the same `first_login`, in RFC 1123 GMT like `last_login` |

## Expected Final State

The persisted timestamps are exposed consistently and only to members.

## Pass/Fail Criteria

**Pass:**
- Stable ISO/RFC 1123 values, field filter honoured, non-member denied

**Fail:**
- Values change between reads, the filter is ignored, or a non-member receives `created_at`
