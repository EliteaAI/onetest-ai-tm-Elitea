---
id: ELITEA-4552
title: "Settings → Web Search is editable only in the public project, read-only elsewhere"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- User has public-project admin access
- User has access to at least one non-public project, as both a regular member and an admin

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As public-project admin, open Settings → General in the public project | A "Web Search" section exists with a picker listing shared web-search toolkits plus a "None" option |
| 2 | Select a different shared toolkit (or "None") and save | Change saves and is reflected platform-wide |
| 3 | Open Settings → General in a non-public project as a regular member | "Web Search" section shows only a read-only line naming the current platform toolkit, with no edit control |
| 4 | Open the same section in the non-public project as that project's own admin | Same read-only line is shown; no edit control appears despite admin role in that project |
| 5 | Attempt to call the settings-update path directly as a non-public-project admin (e.g. via devtools network request replay) | The write is refused |

## Expected Final State

Only the public project retains write access to the Web Search platform setting; every other project (and every other admin role) sees it as read-only.

## Pass/Fail Criteria

**Pass:**
- Picker and save work only in the public project; all other contexts show read-only text and refuse direct write attempts

**Fail:**
- A non-public project can edit the setting, or the direct write attempt succeeds
