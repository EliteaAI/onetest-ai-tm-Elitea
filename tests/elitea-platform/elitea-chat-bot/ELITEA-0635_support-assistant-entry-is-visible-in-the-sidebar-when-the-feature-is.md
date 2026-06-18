---
id: ELITEA-0635
title: "Support Assistant entry is visible in the sidebar when the feature is enabled"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [feature-flag, presence, sidebar, smoke]
requirements: [EliteaAI/elitea_issues#4780, EliteaAI/elitea_issues#4773]
---
# ELITEA-0635: Support Assistant entry is visible in the sidebar when the feature is enabled

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** When the Support Assistant feature is enabled, a clearly labeled "Support Assistant" entry must be present at the bottom of the sidebar on every page. This is the primary in-sidebar access point and must be discoverable in both expanded and collapsed sidebar states.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant is enabled (Admin → Guardrails → Support Assistant toggle is ON)
User is a regular (non-admin) user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Chat page. | The page loads. The sidebar is visible on the left side with standard navigation items (Chat, Agents, Pipelines, etc.). |
| 2 | Scroll to the bottom of the sidebar and look for any Support Assistant-related entry. | A "Support Assistant" entry is present at the bottom of the sidebar, visually separated from the main navigation group. |
| 3 | Verify it is positioned below the standard navigation items and is not mixed in with them. | The entry is clearly distinct — not grouped with Chat, Agents, Pipelines, etc. |
| 4 | Collapse the sidebar by clicking the collapse control at the top. | The sidebar switches to icon-only mode. |
| 5 | Look for the Support Assistant entry in the collapsed sidebar. | An icon for the Support Assistant entry is visible. Hovering over it shows a tooltip with the text "Support Assistant". |
| 6 | Expand the sidebar again. | The full "Support Assistant" text label reappears next to its icon. |

## Expected Final State

The full "Support Assistant" text label reappears next to its icon.

## Pass/Fail Criteria

Pass: Support Assistant entry is present at the bottom of the sidebar in expanded mode with correct label; Entry has a visible icon and tooltip in collapsed mode; Entry is clearly distinct from the main navigation items.
Fail: No Support Assistant entry in the sidebar; Entry appears in the wrong location; Label is missing or incorrect; Entry disappears or has no icon/tooltip in collapsed sidebar mode.
