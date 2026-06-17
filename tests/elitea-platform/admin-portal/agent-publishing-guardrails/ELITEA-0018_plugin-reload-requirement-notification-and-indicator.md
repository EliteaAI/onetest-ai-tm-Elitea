---
id: ELITEA-0018
title: "Plugin Reload Requirement Notification and Indicator"
priority: critical
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, plugin-reload, guardrails, story:4434, r-2.0.2, admin, p0]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0018: Plugin Reload Requirement Notification and Indicator

**Module:** Agent Publishing Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after toggling "Block Agent Publishing" to ON and clicking Save, the UI displays a "Reload required" indicator and an admin notification/toast message indicating that plugin reload is required to apply changes.

## Preconditions

Admin access to Guardrails configuration
elitea_core plugin is currently loaded and active

## Test Data

Guardrail: "Block Agent Publishing"
Expected notification message: "Changes saved. Plugin reload required to apply."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Locate "Block Agent Publishing" toggle (currently OFF) | Toggle is in OFF state |
| 3 | Click the toggle to switch it to ON | Toggle switches to ON, project exception dropdown appears |
| 4 | Click "Save" button without selecting any exception projects | Save action processes |
| 5 | Observe the UI for a "Reload required" indicator (badge, icon, or text) | "Reload required" indicator appears near the guardrail section or at the top of the page |
| 6 | Observe for admin notification or toast message | Toast/notification appears at top or bottom of page |
| 7 | Read the notification message content | Message displays: "Changes saved. Plugin reload required to apply." (exact or similar wording) |
| 8 | Verify notification auto-dismisses or can be manually dismissed | Notification can be closed or auto-dismisses after a few seconds |
| 9 | Verify "Reload required" indicator persists until plugin is reloaded | Indicator remains visible even after notification is dismissed |
| 10 | Navigate to an agent and check Publish button state | "Publish" button is still enabled (changes not yet applied) |
| 11 | Return to Admin and reload the elitea_core plugin | Plugin reload completes successfully |
| 12 | Check if "Reload required" indicator disappears after reload | Indicator is removed/hidden after successful reload |

## Expected Final State

Indicator is removed/hidden after successful reload

## Pass/Fail Criteria

PASS:
- "Reload required" indicator appears after saving guardrail changes
- Admin notification/toast displays correct message about plugin reload requirement
- Notification can be dismissed or auto-dismisses
- "Reload required" indicator persists until plugin reload is performed
- Changes are NOT applied until plugin is reloaded
- "Reload required" indicator disappears after successful plugin reload

FAIL:
- No "Reload required" indicator appears
- No admin notification/toast appears
- Notification message is incorrect or missing
- Changes are applied immediately without requiring plugin reload
- "Reload required" indicator does not persist or does not disappear after reload
