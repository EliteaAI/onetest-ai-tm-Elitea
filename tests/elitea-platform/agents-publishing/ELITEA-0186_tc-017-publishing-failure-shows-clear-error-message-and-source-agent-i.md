---
id: ELITEA-0186
title: "TC-017: Publishing Failure Shows Clear Error Message and Source Agent Is Unchanged"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0186: TC-017: Publishing Failure Shows Clear Error Message and Source Agent Is Unchanged

**Module:** Agents Publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when publishing fails due to a system/network error, the user sees a clear failure notification (not a success message), the source agent is unmodified, no partial entry appears in Agents Studio, and retrying the publish succeeds.

Coverage:
- Failure notification shown with clear error wording (not "success")
- Source agent configuration unchanged after failed publish
- No partial/broken agent entry created in Agents Studio
- Retry publish succeeds under normal conditions

## Preconditions

- Logged in as User A
- Agent A is configured and has a saved version
- Method to simulate failure: network throttling in browser DevTools, or coordinate with dev team to trigger a backend error

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open browser DevTools Network tab; enable 'Offline' or throttle to block the publish API call | Network blocked |
| 2 | Open Agent A, click Publish, enter 'v1.0-fail-test', check agreement, click Continue → validation runs → click Publish | Publish button clicked; request sent |
| 3 | Observe the UI feedback | An error notification appears; it does NOT say 'published successfully'; it indicates failure |
| 4 | Re-enable network in DevTools | Network restored |
| 5 | Navigate to Agent A in the project | Agent A configuration is unchanged from before the failed publish attempt |
| 6 | Navigate to Agents Studio, search for Agent A version 'v1.0-fail-test' | No partial or broken entry for 'v1.0-fail-test' exists in Studio |
| 7 | Retry the publish with normal network: click Publish, enter 'v1.0-fail-test', agree, run validation, publish | Publish succeeds; success notification shown; Agent A appears in Studio |

## Expected Final State

Publish succeeds; success notification shown; Agent A appears in Studio

## Pass/Fail Criteria

PASS:
- Clear failure error notification shown (not success)
- Source agent is unchanged after the failed attempt
- No partial publish artifact in Agents Studio
- Retry publish succeeds

FAIL:
- Error notification says "published successfully" despite failure
- Agent A configuration is altered by the failed publish
- A broken/partial Agent A entry appears in Agents Studio after the failed attempt
- Retry publish also fails despite restored network
