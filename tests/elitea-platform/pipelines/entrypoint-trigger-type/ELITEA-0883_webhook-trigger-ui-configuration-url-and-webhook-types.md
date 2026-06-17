---
id: ELITEA-0883
title: "Webhook Trigger — UI Configuration, URL, and Webhook Types"
priority: high
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, webhook, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0883: Webhook Trigger — UI Configuration, URL, and Webhook Types

**Module:** Entrypoint Trigger Type · **Priority:** High · **Type:** Functional

**Objective:** Verifies that selecting Webhook shows all required UI fields (Webhook Type, Webhook URL, Secret Value), that the default type is Custom, that the URL format is correct and changes with type selection, that the copy button works, and that Custom type shows the correct description.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node is open in edit mode
Pipeline has been saved at least once (version ID exists for URL generation)

## Test Data

Pipeline project ID and version ID (obtain from URL or API)
Expected URL pattern: .../webhook/prompt_lib/{project_id}/{version_id}/{type}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Entrypoint node config and select 'Webhook' from the Trigger dropdown | Webhook configuration section appears below the dropdown |
| 2 | Inspect all fields in the Webhook configuration section | Three fields are visible: Webhook Type selector, Webhook URL (read-only display), Secret Value field (auto-generated, read-only/copyable) |
| 3 | Check the default value in the Webhook Type selector | Default type is 'Custom' |
| 4 | Observe the Webhook URL displayed | URL follows the format .../webhook/prompt_lib/{project_id}/{version_id}/custom with the correct project and version IDs |
| 5 | Click the copy button next to the Webhook URL | URL is copied to clipboard (confirm by pasting elsewhere) |
| 6 | Read the description shown for the Custom type | Description states something equivalent to: 'Uses X-Webhook-Token header with secret token' |
| 7 | Change the Webhook Type to 'GitHub' | URL suffix changes to /github; the URL now ends with /github |
| 8 | Change the Webhook Type to 'GitLab' | URL suffix changes to /gitlab; the URL now ends with /gitlab |
| 9 | Change the Webhook Type back to 'Custom' | URL suffix reverts to /custom |
| 10 | Observe the Secret Value field — it is auto-generated and displayed (read-only or copyable); copy it for use in subsequent tests; save the pipeline | Secret value is auto-generated and displayed; pipeline saves successfully |

## Expected Final State

Secret value is auto-generated and displayed; pipeline saves successfully

## Pass/Fail Criteria

PASS: All three fields present; default is Custom; URL format matches expected pattern; URL updates with type; copy works; Custom description accurate
FAIL: Missing fields; wrong default; URL format incorrect; URL does not update on type change; copy button non-functional
