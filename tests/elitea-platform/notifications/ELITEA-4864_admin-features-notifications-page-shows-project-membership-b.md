---
id: ELITEA-4864
title: "Admin Features Notifications page shows Project Membership block with two toggles"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:notifications, issue:7340, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7340"]
---

# ELITEA-4864: Admin Features Notifications page shows Project Membership block with two toggles

**Module:** admin-portal · **Priority:** critical · **Type:** functional

**Objective:** Verify the new Notifications page in Admin → Features opens and shows the Project Membership block with both membership toggles.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Logged in to `{{base_url}}` as a platform admin with access to the Admin portal.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Admin portal and expand **FEATURES → Features** | Features page loads; sub-nav lists Chat, Skills, Publishing, MCPs, Cost & Usage, Schedules, Webhooks and **Notifications**. |
| 2 | Click **Notifications** | URL ends with `#notifications`; block **Project Membership** with a bell icon and label "2 settings" is shown. |
| 3 | Collapse the block with the chevron, then expand it again | Block collapses and expands; content is unchanged. |
| 4 | Inspect the block content | Two toggle cards with descriptions: "Notify users when added to a team project" and "Notify users when removed from a team project". |
| 5 | Reload the page | Page reopens on Notifications; no console errors. |

---

## Expected Final State

The Notifications page is reachable and shows the Project Membership block with both toggles.

---

## Pass/Fail Criteria

**Pass:**
- Page, block and both toggle cards render
- Reload keeps the Notifications section

**Fail:**
- Notifications item missing or page blank/error
- A toggle card is missing
- Console errors on load
