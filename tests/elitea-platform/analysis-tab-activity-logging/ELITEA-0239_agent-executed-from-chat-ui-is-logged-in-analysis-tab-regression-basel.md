---
id: ELITEA-0239
title: "Agent executed from Chat UI is logged in Analysis tab — regression baseline"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0239: Agent executed from Chat UI is logged in Analysis tab — regression baseline

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that agent invocations triggered from the Chat UI continue to be logged in the Analysis tab as stated in the bug report — this is the known-working regression baseline.

**Coverage:**
- Chat UI-triggered agent call appears in Analysis tab
- Existing working path is not broken by the fix for API logging
- Log entry contains correct agent name and timestamp metadata

## Preconditions

- Logged in to {{base_url}}
- A published Agent exists in the current project
- Chrome or Edge, latest stable version

## Test Data

- Chat message: `"Hello, this is a Chat UI baseline test."`
- Agent: any published Agent in the current project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Start a new conversation. Add the target Agent as a participant or open Agent Chat directly. | New conversation started with the agent active. |
| 2 | Send message: `"Hello, this is a Chat UI baseline test."` | Agent processes the message and returns a response. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens with the activity log visible. |
| 4 | Locate the entry for the just-completed chat invocation (filter by timestamp or agent name). | Entry is present with correct agent name, timestamp within 60 seconds, and Chat source indication. |

## Expected Final State

Entry is present with correct agent name, timestamp within 60 seconds, and Chat source indication.

## Pass/Fail Criteria

**Pass:**
- Entry for the Chat UI call is present in Analysis tab
- Existing Chat logging behavior is unaffected after the API logging fix

**Fail:**
- Chat-triggered calls no longer appear (regression introduced by the fix)
- Entry present but missing agent name or timestamp
