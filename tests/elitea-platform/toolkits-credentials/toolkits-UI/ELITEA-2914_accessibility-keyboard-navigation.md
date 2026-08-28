---
id: ELITEA-2914
title: "Accessibility — Keyboard Navigation"
priority: low
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, accessibility, keyboard]
requirements: []
---
# ELITEA-2914: Accessibility — Keyboard Navigation

**Module:** Toolkits & Indexes · **Priority:** Low · **Type:** Functional

**Objective:** Verify a keyboard-only user can reach and operate the breadcrumbs, Configuration/Activity tabs, "Delete Index", and "Select Tool" without a mouse.

**Coverage:**
- Tab-key focus order through breadcrumbs and tabs
- Enter activates the focused tab
- "Delete Index" is reachable, labeled, and operable via keyboard, including its confirmation modal
- "Select Tool" is reachable and operable via keyboard

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing Index with completed indexing data

## Test Data

| Field | Value |
|-------|-------|
| Index | Any completed Index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index details page and press Tab repeatedly, without using a mouse. | Focus moves through the breadcrumbs, then "Configuration" and "Activity", in a visible, logical order. |
| 2 | With a tab focused, press Enter. | That tab becomes selected. |
| 3 | Continue tabbing to "Delete Index". | "Delete Index" receives visible focus and has an accessible label or tooltip. |
| 4 | Press Enter on "Delete Index". | Confirmation modal opens. |
| 5 | Tab to the modal's cancel action and press Enter. | Modal closes without deleting the Index. |
| 6 | Navigate to the Search page and press Tab until "Select Tool" receives focus. | "Select Tool" receives visible focus. |
| 7 | Press Enter or the Down arrow key on "Select Tool". | Tool list opens. |

## Expected Final State

Every tested control is reachable and operable via keyboard alone, with visible focus indication throughout.

## Pass/Fail Criteria

**Pass:**
- All tested controls are keyboard-reachable in a logical order
- Enter activates each focused control
- "Delete Index" has an accessible label/tooltip and its modal is keyboard-operable

**Fail:**
- Any tested control is unreachable via keyboard
- Enter fails to activate a focused control
- "Delete Index" lacks an accessible label/tooltip, or its modal cannot be operated via keyboard
