---
id: ELITEA-0634
title: "No Support Assistant entry or launcher appears when the feature is disabled"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [disabled-state, not-hardwired, feature-flag]
requirements: [#4780]
---
# ELITEA-0634: No Support Assistant entry or launcher appears when the feature is disabled

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** The Support Assistant must not be hard-wired into the sidebar. When the feature is disabled — whether through the build-time flag or Admin Guardrails — no Support Assistant entry in the sidebar and no floating launcher icon should be visible to any user on any page.

## Preconditions

Logged in to ELITEA on a test environment where Support Assistant is disabled (either VITE_ELITEA_ASSISTANT build flag is false/unset, or Admin has turned the Support Assistant toggle OFF in Admin → Guardrails)
Logged in as a regular (non-admin) user

## Test Data

Environment with Support Assistant disabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as a regular user and navigate to the Chat page. | Page loads. Sidebar is visible. |
| 2 | Inspect the entire sidebar from top to bottom. | No "Support Assistant" entry appears anywhere in the sidebar. |
| 3 | Look at the bottom-left area of the page for a floating launcher icon. | No floating launcher icon is present. |
| 4 | Navigate to the Agents, Pipelines, and Credentials pages one by one. | On all three pages: no Support Assistant sidebar entry and no floating launcher icon. |

## Expected Final State

On all three pages: no Support Assistant sidebar entry and no floating launcher icon.

## Pass/Fail Criteria

Pass: No Support Assistant sidebar entry on any page; No floating launcher icon on any page.
Fail: A "Support Assistant" entry or floating launcher is visible when the feature is disabled; The entry is hidden but still occupies space; The widget can be accessed through any UI element when it should be disabled.
