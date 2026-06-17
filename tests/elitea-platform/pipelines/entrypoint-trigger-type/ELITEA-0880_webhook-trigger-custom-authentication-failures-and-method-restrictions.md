---
id: ELITEA-0880
title: "Webhook Trigger (Custom) — Authentication Failures and Method Restrictions"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [negative-testing, error-handling, pipeline, security, webhook, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0880: Webhook Trigger (Custom) — Authentication Failures and Method Restrictions

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that requests with missing or incorrect authentication are rejected with HTTP 401/403, and that non-POST HTTP methods to the webhook URL are rejected with HTTP 405.

## Preconditions

A pipeline with Custom Webhook trigger configured and saved
The webhook URL is known; the auto-generated secret has been copied from the UI Webhook config
A tool to send HTTP requests is available (curl, Postman)

## Test Data

Webhook URL: {base_url}/webhook/prompt_lib/{project_id}/{version_id}/custom
Correct secret: (auto-generated value — copy from UI Webhook settings)
Wrong secret: wrong-secret-value

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a POST request to the webhook URL with NO 'X-Webhook-Token' header | HTTP 401 or 403 response is returned; pipeline does NOT execute |
| 2 | Send a POST request with 'X-Webhook-Token: wrong-secret-value' (incorrect secret) | HTTP 401 or 403 response is returned; pipeline does NOT execute |
| 3 | Send a GET request to the webhook URL | HTTP 405 (Method Not Allowed) is returned or 503 Service Unavailable |
| 4 | Send a PUT request to the webhook URL | HTTP 405 (Method Not Allowed) is returned or 503 Service Unavailable |
| 5 | Send a DELETE request to the webhook URL | HTTP 405 (Method Not Allowed) is returned or 503 Service Unavailable |
| 6 | Verify that the pipeline run history shows no new entries for any of the rejected requests | No spurious run entries appear in run history |

## Expected Final State

No spurious run entries appear in run history

## Pass/Fail Criteria

PASS: Missing token -> 401/403; wrong token -> 401/403; GET/PUT/DELETE -> 405; no run history entries for rejected requests
FAIL: Requests with missing/wrong token succeed; non-POST methods accepted; pipeline executes on rejected request
