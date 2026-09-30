---
id: ELITEA-3415
title: "GitLab Signing Token: Valid webhook-signature HMAC Is Accepted"
priority: high
type: functional
module: webhooks
status: draft
execution_type: manual
tags: [feat:pipelines, int:gitlab, story:5097, webhooks]
requirements: [EliteaAI/elitea_issues#5097]
---
# ELITEA-3415: GitLab Signing Token — Valid Signature Accepted

**Module:** Webhooks · **Priority:** High · **Type:** Functional

**Objective:** Confirm a pipeline trigger configured for GitLab's "Signing token" method accepts a real GitLab delivery whose `webhook-signature` header is a valid HMAC-SHA256 over `{webhook-id}.{webhook-timestamp}.{raw_body}`, computed with the configured signing secret.

**Coverage:** AC — `webhook-signature` HMAC-SHA256 validation for the signing token method

## Preconditions

- A pipeline with a GitLab webhook trigger configured
- Trigger's auth method set to "Signing token", with a GitLab-generated signing secret (`whsec_...`) pasted in
- A GitLab repository/project with a webhook pointed at the trigger URL, configured with the same signing token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In GitLab, trigger a real webhook delivery (e.g. push a commit) to the configured webhook URL. | GitLab sends a request with `webhook-id`, `webhook-timestamp`, and `webhook-signature` headers. |
| 2 | Observe the pipeline trigger's execution/delivery log. | The request is accepted; the pipeline run starts. |
| 3 | In GitLab's webhook delivery view, check the response status for the request. | 2xx success response recorded. |

## Expected Final State

A correctly signed GitLab delivery is validated and triggers the pipeline normally.

## Pass/Fail Criteria

**Pass:**
- Valid signed delivery is accepted and the pipeline runs

**Fail:**
- Valid signed delivery is rejected (e.g. 401/403), or the pipeline does not run
