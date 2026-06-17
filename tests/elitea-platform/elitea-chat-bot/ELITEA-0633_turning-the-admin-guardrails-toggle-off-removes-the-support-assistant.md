---
id: ELITEA-0633
title: "Turning the Admin Guardrails toggle OFF removes the Support Assistant from the sidebar for regular users"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [admin-control, guardrails, sidebar, toggle]
requirements: [#4780, #4781]
---
# ELITEA-0633: Turning the Admin Guardrails toggle OFF removes the Support Assistant from the sidebar for regular users

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** An admin disabling the Support Assistant in Guardrails must immediately result in the entry and launcher disappearing for all regular users.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant is currently enabled and visible to regular users
Platform Admin credentials are available
A separate regular user account is available for verification

## Test Data

Platform Admin account; Regular user account

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as a Platform Admin. Navigate to Admin → Guardrails → Support Assistant section. | The Support Assistant toggle is currently ON. |
| 2 | Turn the Support Assistant toggle to OFF and save the configuration. | The toggle is saved as disabled. A confirmation or success indicator is shown. |
| 3 | Log out and log back in as the regular user. Navigate to the Chat page. | Login succeeds. Chat page loads. |
| 4 | Check the sidebar top to bottom for any Support Assistant entry. | No "Support Assistant" entry is present anywhere in the sidebar. |
| 5 | Check for the floating launcher icon on the page. | No launcher icon is visible. |
| 6 | Navigate to Agents and Pipelines pages to verify the same. | No Support Assistant entry or launcher on any page while the toggle is OFF. |
| 7 | Log back in as Platform Admin. Turn the Support Assistant toggle back ON and save. | Toggle is restored to enabled. |
| 8 | Log in again as the regular user and navigate to the Chat page. | The Support Assistant sidebar entry and launcher are visible again. |

## Expected Final State

The Support Assistant sidebar entry and launcher are visible again.

## Pass/Fail Criteria

Pass: Sidebar entry and launcher disappear for regular users after admin disables the toggle; Sidebar entry and launcher reappear after admin re-enables the toggle.
Fail: Sidebar entry or launcher remains visible after the admin disables the toggle; The toggle change has no visible effect for regular users.
