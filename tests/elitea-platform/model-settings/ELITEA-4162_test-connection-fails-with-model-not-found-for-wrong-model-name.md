---
id: ELITEA-4162
title: "Test connection fails with Model not found for wrong model name despite valid credential, recognition indicator agrees"
priority: critical
type: functional
module: model-settings
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- A saved, valid non-DIAL AI credential exists in the project.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| Invalid Model Name variants | A misspelled/non-existent model id, and a garbage string containing a real model token as a substring (e.g. `weomfowemfom gpt-5.6elg erlg krem`) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the LLM model form, select the valid credential | Credential selected. |
| 2 | Enter an invalid Model Name (both variants, in turn) | Field accepts input. |
| 3 | Observe recognition indicator for each variant | Shows "Not recognized..." — not falsely "Recognized". |
| 4 | Click Test connection | Result returned. |
| 5 | Observe result | "Model not found" category with sanitized message. |
| 6 | Inspect message/network response | No API key, hostname/IP, or stack trace. |
| 7 | Compare recognition state (step 3) vs. result (step 5) | Both agree the name is invalid. |

## Expected Final State

Test connection reports "Model not found" and the recognition indicator correctly shows "Not recognized" for both invalid variants.

## Pass/Fail Criteria

**Pass:**
- "Model not found" shown with sanitized message.
- Recognition indicator agrees (Not recognized) for both variants.

**Fail:**
- Wrong category shown, or sensitive data exposed.
- Recognition indicator falsely shows "Recognized".
