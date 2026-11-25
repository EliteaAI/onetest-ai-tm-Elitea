---
id: ELITEA-4553
title: "Shared with all projects switch is public-project/admin-only and requires a non-private credential"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Public-project admin access
- A toolkit in a non-public project
- A Tavily toolkit in the public project currently referencing a private credential

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a toolkit's configuration in a non-public (Team/Private) project | No "Shared with all projects" switch is present |
| 2 | Open a toolkit's configuration in the public project as a non-admin member | Switch is not visible or not editable |
| 3 | Open a toolkit's configuration in the public project as an admin | Switch IS visible and editable |
| 4 | On the public-project Tavily toolkit with a private credential reference, attempt to enable "Shared with all projects" | System blocks the action with a validation error |
| 5 | Change the credential reference to a non-private one, then enable the switch | Switch saves successfully |
| 6 | Open Settings → Web Search picker in the public project | The toolkit now appears as a selectable option |

## Expected Final State

The toolkit is now properly shared (non-private credential reference, switch ON) and appears in the Settings → Web Search picker.

## Pass/Fail Criteria

**Pass:**
- Switch visibility/editability is correctly restricted; private-credential toolkits are blocked from sharing until fixed

**Fail:**
- The switch appears outside the public project, is editable by a non-admin, or saves successfully with a private credential reference
