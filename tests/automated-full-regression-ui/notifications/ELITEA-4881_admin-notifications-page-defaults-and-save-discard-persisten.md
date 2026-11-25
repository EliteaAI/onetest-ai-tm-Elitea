---
id: ELITEA-4881
title: "Admin Notifications page defaults and Save Discard persistence"
priority: critical
type: regression
module: admin-portal
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4881: Admin Notifications page defaults and Save Discard persistence

**Module:** admin-portal · **Priority:** critical · **Type:** regression

**Objective:** Regression of Admin → Features → Notifications: the Project Membership block renders with both toggles, defaults are add on / remove off, and Save/Discard work and persist. Manual source: ELITEA-4864, ELITEA-4865, ELITEA-4880.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features#notifications` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Admin → Features and click **Notifications** | Project Membership block with "2 settings" and both toggle cards is shown. |
| 2 | On an environment where flags were never saved, check both toggles | Add toggle on, remove toggle off. |
| 3 | Without changes, check the action bar | Save and Discard are disabled. |
| 4 | Switch the remove toggle, then click **Discard** | Toggle returns to its saved value; buttons disabled. |
| 5 | Switch the remove toggle and click **Save**, then reload | New value persists after reload. |
| 6 | Restore the original value and save | Original state restored. |

---

## Expected Final State

Notifications page works and toggles are at their original values.

---

## Pass/Fail Criteria

**Pass:**
- Block and toggles render with correct defaults
- Discard reverts, Save persists

**Fail:**
- Page or toggles missing
- Wrong defaults
- Discard or Save broken
