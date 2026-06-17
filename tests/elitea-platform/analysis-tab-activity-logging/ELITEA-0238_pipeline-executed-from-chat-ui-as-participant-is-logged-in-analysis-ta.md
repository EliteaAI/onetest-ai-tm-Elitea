---
id: ELITEA-0238
title: "Pipeline executed from Chat UI (as participant) is logged in Analysis tab — regression baseline"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0238: Pipeline executed from Chat UI (as participant) is logged in Analysis tab — regression baseline

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that Pipeline executions triggered via the Chat UI (pipeline added as a participant) are logged in the Analysis tab — regression baseline for pipelines.

**Coverage:**
- Chat-triggered pipeline call appears in Analysis tab
- Existing working Chat path for pipelines is not broken by the API logging fix
- Log entry contains correct pipeline name and timestamp

## Preconditions

- Logged in to {{base_url}}
- A published Pipeline exists in the current project, configured to accept chat input
- Chrome or Edge, latest stable version

## Test Data

- Chat message: `"Run pipeline — Chat UI logging baseline test."`
- Pipeline: any published Pipeline in the current project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Start a new conversation. Add the target Pipeline as a participant. | Conversation started with the pipeline participant active. |
| 2 | Send message: `"Run pipeline — Chat UI logging baseline test."` | Pipeline executes and returns output in the chat. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens showing activity log. |
| 4 | Locate the entry for the pipeline invocation (filter by timestamp or pipeline name). | Entry is present with correct pipeline name, timestamp within 60 seconds, and Chat source. |

## Expected Final State

Entry is present with correct pipeline name, timestamp within 60 seconds, and Chat source.

## Pass/Fail Criteria

**Pass:**
- Chat-triggered pipeline call is logged in Analysis tab
- Existing Chat pipeline logging is unaffected by the fix

**Fail:**
- No entry for Chat pipeline invocation (Chat logging regressed)
- Pipeline entries only appear when triggered via the API after the fix
