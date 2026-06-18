---
id: ELITEA-0626
title: "Support Assistant floating launcher is visible on every main application page"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [cross-page, story:4774, presence, launcher, r-2.0.3, smoke]
requirements: [4774, 4773]
---
# ELITEA-0626: Support Assistant floating launcher is visible on every main application page

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the Support Assistant is enabled, the floating launcher button/icon is consistently visible on every main application section: Chat, Agents, Pipelines, Credentials, Toolkits, Applications, MCPs, Artifacts, and Settings. The launcher must be an independent UI element, not embedded in the sidebar navigation.

## Preconditions

Platform Admin has enabled the Support Assistant toggle in Admin → Guardrails.
The tester is logged in as a regular (non-admin) user.
The browser viewport is 1280×800 or larger.

## Test Data

User account: regular user (non-admin)
Pages to check: Chat, Agents, Pipelines, Credentials, Toolkits, Applications, MCPs, Artifacts, Settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as a regular user and navigate to the Chat page | A Support Assistant launcher icon/button is visible on the page, separate from the sidebar nav items |
| 2 | Navigate to the Agents page | Launcher is still visible; position is consistent with Chat page |
| 3 | Navigate to the Pipelines page | Launcher is still visible |
| 4 | Navigate to the Credentials page | Launcher is still visible |
| 5 | Navigate to the Toolkits page | Launcher is still visible |
| 6 | Navigate to the Applications page | Launcher is still visible |
| 7 | Navigate to the MCPs page | Launcher is still visible |
| 8 | Navigate to the Artifacts page | Launcher is still visible |
| 9 | Navigate to the Settings page | Launcher is still visible |
| 10 | Confirm the launcher is positioned consistently (does not jump or reflow) across all pages | Launcher anchor position is identical on all pages |

## Expected Final State

Launcher anchor position is identical on all pages

## Pass/Fail Criteria

PASS: Launcher icon is visible on all 9 pages; position is stable.
FAIL: Launcher is missing on any page, or its position shifts/reflows between page navigations.
