---
id: ELITEA-4880
title: "Save and Discard on Admin Notifications settings page"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4880: Save and Discard on Admin Notifications settings page

**Module:** admin-portal · **Priority:** high · **Type:** functional

**Objective:** Verify the action bar Save and Discard follow real changes, Discard reverts and saved values persist.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.
- Current toggle values are noted.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features#notifications` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Notifications page without changes | **Save** and **Discard** are disabled. |
| 2 | Switch the remove toggle | Save and Discard become enabled. |
| 3 | Click **Discard** | Both toggles return to saved values; buttons disabled again. |
| 4 | Switch both toggles and click **Save** | Save confirmation shown; buttons disabled. |
| 5 | Reload the page | New values persist. |
| 6 | Restore the original values and save | Original state restored. |

---

## Expected Final State

Toggles are back at their original values.

---

## Pass/Fail Criteria

**Pass:**
- Buttons enabled only after a change
- Discard reverts
- Saved values survive reload

**Fail:**
- Buttons enabled without a change
- Discard does not revert
- Values lost after reload
