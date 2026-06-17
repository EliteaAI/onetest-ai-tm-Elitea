---
id: ELITEA-0869
title: "Webhook URL Uniqueness Across Pipelines in the Same Project"
priority: medium
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, security, webhook, R-2.0.3, trigger]
requirements: [EliteaAI/elitea_issues#4827]
---
# ELITEA-0869: Webhook URL Uniqueness Across Pipelines in the Same Project

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that two pipelines configured with Webhook triggers within the same project have unique webhook URLs, preventing one pipeline's webhook from accidentally triggering another.

## Preconditions

User is logged in with pipeline edit permissions
Two pipelines exist (or can be created) in the same project, each with an Entrypoint node
Both pipelines are configured with Webhook triggers

## Test Data

Pipeline X: Webhook trigger configured
Pipeline Y: Webhook trigger configured (different pipeline, same project)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline X in edit mode, navigate to the Entrypoint node Webhook config, and copy the Webhook URL | Pipeline X Webhook URL is noted |
| 2 | Open Pipeline Y in edit mode, navigate to the Entrypoint node Webhook config, and copy the Webhook URL | Pipeline Y Webhook URL is noted |
| 3 | Compare the two Webhook URLs | The URLs are different — at minimum the {version_id} component differs; the URLs cannot be identical |
| 4 | Send a POST request to Pipeline X's webhook URL with Pipeline X's auto-generated secret (copied from its Webhook config UI) | Only Pipeline X is triggered; Pipeline Y run history shows no new entry |
| 5 | Send a POST request to Pipeline Y's webhook URL with Pipeline Y's auto-generated secret (copied from its Webhook config UI) | Only Pipeline Y is triggered; Pipeline X run history shows no new entry |

## Expected Final State

Only Pipeline Y is triggered; Pipeline X run history shows no new entry

## Pass/Fail Criteria

PASS: Webhook URLs are unique between pipelines; each webhook triggers only its own pipeline
FAIL: Webhook URLs are the same or one URL triggers multiple pipelines
