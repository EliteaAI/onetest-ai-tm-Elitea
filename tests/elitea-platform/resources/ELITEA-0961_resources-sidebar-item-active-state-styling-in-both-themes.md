---
id: ELITEA-0961
title: "Resources Sidebar Item Active State Styling in Both Themes"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0961: Resources Sidebar Item Active State Styling in Both Themes

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Resources" left sidebar item displays a visually distinct active/selected state when the Resources page is open, in both Dark and Light Modes, and reverts to inactive state when navigating away.

**Coverage:**
- Active state styling in Dark Mode
- Active state styling in Light Mode
- Inactive state restored when navigating away from Resources

## Preconditions

Logged in to ELITEA; on the Resources page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page in Dark Mode. | Resources page loads. |
| 2 | Inspect the "Resources" item in the left sidebar. | "Resources" sidebar item has a visually distinct active/selected state (e.g., highlighted background, bold text, or icon change) that differentiates it from non-active sidebar items. |
| 3 | Switch to Light Mode. | Theme switches to Light Mode; still on Resources page. |
| 4 | Inspect the "Resources" item in the left sidebar again in Light Mode. | "Resources" sidebar item still shows an active/selected state in Light Mode. |
| 5 | Navigate to a different page (e.g., Chat or Agents). | "Resources" sidebar item returns to its default inactive state. |

## Expected Final State

"Resources" sidebar item returns to its default inactive state.

## Pass/Fail Criteria

**Pass:**
- "Resources" sidebar item shows a visually distinct active state in Dark Mode (e.g., highlighted background, bold text, or active icon)
- "Resources" sidebar item shows a visually distinct active state in Light Mode
- "Resources" sidebar item reverts to inactive state when a different page is active

**Fail:**
- "Resources" sidebar item has no visible active/selected state in either theme
- Active styling persists after navigating away from Resources
- Active styling differs significantly between Dark and Light modes without justification
