---
id: ELITEA-4976
title: "Project created and First login follow the browser time zone and locale like Last login"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** All three dates use the same formatter as Last login in a non-default time zone and locale.

## Preconditions

- User is logged in to `{{base_url}}`
- Chrome DevTools → **Sensors**: Location = Other, Timezone ID `America/Los_Angeles`, Locale `en-GB` (reload after setting)

## Test Data

| Field | Value |
|-------|-------|
| Time zone | America/Los_Angeles (UTC−7 in summer, −8 in winter) |
| Locale | en-GB |
| Oracle | `GET {{base_url}}/api/v2/auth/user/default`, `GET {{base_url}}/api/v2/elitea_core/project_info/prompt_lib/{project_id}/project-info` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **Profile** | First login and Last login are in en-GB 24 h format `DD/MM/YYYY, HH:mm:ss` |
| 2 | Compare First login with the API `first_login` | Equals the UTC value shifted to Los Angeles time (e.g. `09:51:50 GMT` in May → `02:51:50`) |
| 3 | Open Settings → **General** | Project created uses the same `DD/MM/YYYY, HH:mm:ss` format and equals `created_at` in Los Angeles time |
| 4 | Reset the Sensors overrides | Dates return to the default locale and time zone |

## Expected Final State

The three dates are rendered consistently with Last login in any locale and time zone.

## Pass/Fail Criteria

**Pass:**
- Same format and time zone conversion for First login, Last login and Project created

**Fail:**
- One of the fields keeps UTC, a different format or a different locale
