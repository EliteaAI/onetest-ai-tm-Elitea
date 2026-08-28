---
id: ELITEA-2846
title: "ask_user - Headless/API mode with auto_skip returns defaults without hanging"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2846: ask_user - Headless/API mode with auto_skip returns defaults without hanging

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in headless/API mode with auto_skip enabled, tool returns reasonable defaults without hanging.

## Preconditions

- API access is configured
- ask_user tool is enabled for API usage
- auto_skip parameter is available

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `{{api_base_url}}/v1/chat/completions` |
| auto_skip | true |
| Initial prompt | "Create a marketing campaign" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send API request with auto_skip=true | Request is accepted |
| 2 | Trigger agent that would normally call ask_user | Agent executes without UI prompt |
| 3 | Monitor API response time | Response completes within reasonable timeout (< 30s) |
| 4 | Verify response does not hang waiting for user input | Response is returned |
| 5 | Examine response content | Agent uses reasonable default values |
| 6 | Verify response indicates defaults were used | Response mentions assumptions or defaults |
| 7 | Send follow-up API request without auto_skip | Request fails or returns error indicating UI required |

## Expected Final State

Headless mode with auto_skip allows agent to proceed with defaults without requiring user interaction.

## Pass/Fail Criteria

**Pass:** API request completes without hanging, reasonable defaults used, response is coherent, auto_skip flag controls behavior

**Fail:** Request hangs, no response received, unreasonable defaults, auto_skip flag has no effect
