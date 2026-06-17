---
id: ELITEA-0879
title: "Webhook Trigger (GitHub Type) — HMAC Signature Validation"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, security, webhook, R-2.0.3, trigger, github]
requirements: [#4827]
---
# ELITEA-0879: Webhook Trigger (GitHub Type) — HMAC Signature Validation

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that a POST to the GitHub webhook URL with a valid HMAC-SHA256 signature triggers the pipeline, that an invalid or tampered HMAC is rejected, and that a missing signature header is rejected.

## Preconditions

A pipeline with GitHub Webhook trigger configured and saved
The GitHub webhook URL (ending in /github) and auto-generated secret has been copied from the UI Webhook config
Ability to compute HMAC-SHA256: sha256=HMAC-SHA256(secret, body)

## Test Data

Webhook URL: {base_url}/webhook/prompt_lib/{project_id}/{version_id}/github
Secret: (auto-generated value — copy from UI Webhook settings for this pipeline version)
Body: {\"ref\": \"refs/heads/main\", \"commits\": []}
Valid signature: computed as sha256=<hmac_hex> of body using the secret
Invalid signature: sha256=aaabbbcccddd000 (tampered)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Compute HMAC-SHA256 of the request body using the auto-generated secret copied from the UI | Signature computed: sha256=<correct_hmac> |
| 2 | Send a POST to the GitHub webhook URL with header 'X-Hub-Signature-256: sha256=<correct_hmac>' and the body | HTTP 2xx response returned; pipeline execution is triggered |
| 3 | Navigate to run history and confirm pipeline executed successfully | Run appears in history with a trigger notification |
| 4 | Send a POST with 'X-Hub-Signature-256: sha256=aaabbbcccddd000' (tampered/invalid HMAC) | HTTP 401 or 403 returned; pipeline does NOT execute |
| 5 | Send a POST with NO 'X-Hub-Signature-256' header | HTTP 401 or 403 returned; pipeline does NOT execute |
| 6 | Confirm the GitHub webhook URL ends with '/github' | URL path suffix is /github |

## Expected Final State

URL path suffix is /github

## Pass/Fail Criteria

PASS: Valid HMAC -> 2xx + pipeline executes; tampered HMAC -> 401/403; missing header -> 401/403; URL ends with /github
FAIL: Invalid HMAC accepted; missing header accepted; pipeline fires on rejected request; URL suffix wrong
