---
id: ELITEA-0621
title: "Support Assistant displays the configured name, avatar, and branding"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [story:4774, branding, r-2.0.3, config, theme]
requirements: [4774, 4776]
---
# ELITEA-0621: Support Assistant displays the configured name, avatar, and branding

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Support Assistant panel header displays the assistant name and avatar/icon as configured by the admin (not hardcoded defaults). This confirms that the frontend fetches and applies backend-driven configuration for branding.

## Preconditions

Support Assistant is enabled and an active Agent is configured in Admin → Guardrails.
The admin has set a specific assistant name (e.g., "Elitea Assistant") and avatar.

## Test Data

Configured assistant name (note the exact value from admin config before testing)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as a regular user and open the Support Assistant panel | Panel opens |
| 2 | Inspect the panel header/title area | The configured assistant name (e.g., "Elitea Assistant") is displayed — not a generic default like "Chat Bot" |
| 3 | Check for the presence of an avatar/icon in the panel header | An avatar or icon representing the assistant is shown |
| 4 | Log in as Platform Admin, change the assistant name in Admin → Guardrails → Support Assistant config | Config saved |
| 5 | In a regular user session (refresh page if needed), open the Support Assistant | The new assistant name is displayed in the panel header |

## Expected Final State

The new assistant name is displayed in the panel header

## Pass/Fail Criteria

PASS: Panel header shows configured name and avatar; name update from admin is reflected.
FAIL: Hardcoded name shown regardless of config; avatar missing; name change not reflected.
