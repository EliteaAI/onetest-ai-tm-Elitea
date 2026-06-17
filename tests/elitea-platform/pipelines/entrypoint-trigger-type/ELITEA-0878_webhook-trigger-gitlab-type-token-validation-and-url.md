---
id: ELITEA-0878
title: "Webhook Trigger (GitLab Type) — Token Validation and URL"
priority: medium
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, webhook, R-2.0.3, trigger, gitlab]
requirements: [#4827]
---
# ELITEA-0878: Webhook Trigger (GitLab Type) — Token Validation and URL

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that a POST to the GitLab webhook URL with a valid GitLab token triggers the pipeline, that a missing or wrong token is rejected, and that the URL ends with /gitlab.

## Preconditions

A pipeline with GitLab Webhook trigger configured and saved
The GitLab webhook URL (ending in /gitlab) and auto-generated token has been copied from the UI Webhook config
Ability to send HTTP requests with custom headers (curl or Postman)

## Test Data

Webhook URL: {base_url}/webhook/prompt_lib/{project_id}/{version_id}/gitlab
GitLab token header: determined by the UI example (e.g., X-Gitlab-Token)
Valid token: auto-generated value — copy from UI Webhook settings
Wrong token: wrong-gitlab-token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the GitLab webhook URL ends with '/gitlab' | URL path suffix is /gitlab |
| 2 | Send a POST request to the GitLab webhook URL with the correct GitLab token header and value | HTTP 2xx response returned; pipeline execution is triggered |
| 3 | Navigate to run history and confirm pipeline executed successfully | Run appears in history with a trigger notification/label |
| 4 | Send a POST with an incorrect/wrong token value | HTTP 401 or 403 returned; pipeline does NOT execute |
| 5 | Send a POST with no token header | HTTP 401 or 403 returned; pipeline does NOT execute |

## Expected Final State

HTTP 401 or 403 returned; pipeline does NOT execute

## Pass/Fail Criteria

PASS: Correct token -> 2xx + pipeline executes; wrong token -> 401/403; missing token -> 401/403; URL ends /gitlab; run history shows trigger notification
FAIL: Wrong token accepted; missing token accepted; URL suffix wrong
