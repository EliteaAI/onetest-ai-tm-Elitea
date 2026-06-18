---
id: ELITEA-0622
title: "Support Assistant launcher and panel are absent when the feature is disabled by admin"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [disabled-state, feature-flag, guardrails, story:4774, r-2.0.3]
requirements: [4774, 4773]
---
# ELITEA-0622: Support Assistant launcher and panel are absent when the feature is disabled by admin

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that disabling the Support Assistant via Admin → Guardrails removes the floating launcher and the panel from the UI for all regular users. There must be no residual entry point — the feature must not be hard-wired into the UI.

## Preconditions

Two browser sessions available: one as Platform Admin, one as a regular user.
Support Assistant was enabled prior to this test.

## Test Data

Admin account; regular user account

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as Platform Admin; navigate to Admin → Guardrails → Support Assistant section | Support Assistant toggle is visible and currently enabled |
| 2 | Disable the Support Assistant toggle and save | Config saved successfully |
| 3 | In the regular user browser session, refresh the page | Page reloads |
| 4 | Check all main pages (Chat, Agents, Pipelines) for the floating launcher | No launcher icon is visible on any page |
| 5 | Attempt to navigate directly to a Support Assistant URL (if any known URL exists) | No accessible entry point; user cannot open the panel |
| 6 | Re-enable the toggle as admin and save | Toggle is ON again |
| 7 | In the regular user session, refresh the page | Launcher icon reappears |

## Expected Final State

Launcher icon reappears

## Pass/Fail Criteria

PASS: Launcher absent when disabled; returns when re-enabled; existing conversations survive.
FAIL: Launcher still visible when disabled; or conversations are deleted when re-enabling.
