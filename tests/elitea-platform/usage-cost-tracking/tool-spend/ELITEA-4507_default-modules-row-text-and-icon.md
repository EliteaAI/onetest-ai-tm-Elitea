---
id: ELITEA-4507
title: "Default Modules table row for the paid-tool module shows correct text and icon"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4507: Default Modules table row for the paid-tool module shows correct text and icon

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the Web Search (or other paid-tool) row in Settings → General → Default Modules shows the correct title, description, and toggle layout consistent with other module rows (e.g. Image Creation).

**Coverage:**
- Title, description, and icon present and not placeholder/missing
- Chats/Agents toggle columns aligned and labeled consistently with other rows
- Toggles update immediately without a page reload

## Preconditions

- User has access to Settings → General → Default Modules

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → General → Default Modules, locate the paid-tool module row. | Row is present. |
| 2 | Inspect title, description text, and icon. | Title, description ("Let the model search the web and read pages, and cite its sources." or current wording), and icon are present and not placeholder/missing. |
| 3 | Inspect "Chats" and "Agents" toggle columns. | Columns are aligned and labeled consistently with other rows (e.g. Image Creation). |
| 4 | Toggle the switches on/off. | UI reflects the new state immediately (visual on/off state) without requiring a page reload. |

## Expected Final State

The paid-tool module row displays correct, complete content and behaves consistently with other module rows.

## Pass/Fail Criteria

**Pass:**
- Title, description, icon, and toggle layout are all correct and consistent
- Toggles update immediately without reload

**Fail:**
- Any content is missing/placeholder, misaligned, or toggles require a reload to reflect state
