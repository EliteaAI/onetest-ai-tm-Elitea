---
id: ELITEA-2516
title: "Admin role can perform all icon operations upload replace delete"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin role

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| User Role | Admin |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as Admin user | Login successful |
| 2 | Create a new Skill | Creation form opens |
| 3 | Upload a custom icon | Upload succeeds |
| 4 | Save the Skill | Skill created with icon |
| 5 | Edit the Skill | Edit form opens |
| 6 | Replace the icon with a different one | Replace succeeds |
| 7 | Save the Skill | Updated icon saved |
| 8 | Open SelectIconDialog | Dialog opens |
| 9 | Delete an uploaded icon from the gallery | Delete succeeds |
| 10 | Verify all operations completed without permission errors | No errors |

## Expected Final State

Admin users have full access to all Skill icon operations (upload, replace, delete).

## Pass/Fail Criteria

**Pass:**
- Upload succeeds
- Replace succeeds
- Delete succeeds
- No permission errors

**Fail:**
- Any operation fails
- Permission error displayed
