---
id: ELITEA-4969
title: "Clicking First login copies its value like Last login"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7490]
---

**Objective:** First login uses the same click-to-copy behaviour as Last login.

## Preconditions

- User is logged in to `{{base_url}}`
- The browser allows clipboard access for `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{project_id}/settings/profile` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → **Profile** and click the First login value | Toast **"The First login has been copied to the clipboard."** |
| 2 | Paste the clipboard into a text field | Exactly the displayed First login value |
| 3 | Click the Last login value and paste | Last login is copied the same way (control) |

## Expected Final State

First login is copyable exactly as displayed.

## Pass/Fail Criteria

**Pass:**
- Toast shown and clipboard equals the displayed value

**Fail:**
- No toast, nothing copied, or a different value (e.g. raw API format) copied
