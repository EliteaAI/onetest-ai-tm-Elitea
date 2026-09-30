---
id: ELITEA-3416
title: "GitLab Signing Token: Invalid or Stale Signature Is Rejected"
priority: high
type: functional
module: webhooks
status: draft
execution_type: manual
tags: [feat:pipelines, int:gitlab, story:5097, webhooks, security]
requirements: [EliteaAI/elitea_issues#5097]
---
# ELITEA-3416: GitLab Signing Token — Invalid or Stale Signature Rejected

**Module:** Webhooks · **Priority:** High · **Type:** Functional

**Objective:** Confirm the signing-token validation path rejects deliveries with a wrong/tampered `webhook-signature`, and separately rejects deliveries whose `webhook-timestamp` is outside the accepted replay window — both without leaking whether the failure was a bad signature vs. a stale timestamp.

**Coverage:** AC — signing token HMAC validation; replay protection via `webhook-timestamp` recency check

## Preconditions

- A pipeline with a GitLab webhook trigger configured for "Signing token" method
- Ability to send a crafted HTTP request to the trigger URL (e.g. via curl/Postman), reusing headers/body captured from a real GitLab delivery

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Replay a captured request unmodified. | Accepted (baseline sanity check that the captured request is valid). |
| 2 | Replay the same request with the `webhook-signature` value altered (e.g. flip a character). | Request is rejected (401/403); pipeline does not run. |
| 3 | Replay the original request with `webhook-timestamp` changed to a value well outside the configured tolerance (e.g. several hours old), keeping the signature as originally computed for that timestamp (or simply resending the old captured request after the tolerance window has elapsed). | Request is rejected as stale; pipeline does not run. |
| 4 | Compare the error responses from steps 2 and 3. | Both fail closed with a generic error; no response detail distinguishes "bad signature" from "stale timestamp" in a way that would help an attacker. |

## Expected Final State

Neither a tampered signature nor a replayed/stale delivery triggers the pipeline.

## Pass/Fail Criteria

**Pass:**
- Tampered signature is rejected
- Stale timestamp (outside tolerance) is rejected
- Neither leaks distinguishing detail in its error response

**Fail:**
- A tampered signature is accepted and the pipeline runs
- A stale/replayed delivery is accepted and the pipeline runs
