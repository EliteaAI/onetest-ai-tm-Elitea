---
id: ELITEA-0348
title: "extra_params Fields Visible and Functional in Toolkit Test Settings Panel"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0348: extra_params Fields Visible and Functional in Toolkit Test Settings Panel

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the `extra_params` field in the ReadFile Toolkit Test Settings panel accepts a valid JSON string containing the new `extracted_images_names`, `read_images_only`, and `prompt` keys.

**Coverage:**
- `extra_params` field presence and visibility in the UI
- JSON string input accepted without validation error
- Functional execution with all three new keys

## Preconditions

- Logged in to dev environment
- Artifact Toolkit configured with ReadFile enabled
- Navigate to Toolkit settings → ReadFile → Test Settings
- `docx_with_images.docx` in bucket `test`

## Test Data

extra_params JSON: {\"extracted_images_names\": [\"image1.jpeg\"], \"read_images_only\": true, \"prompt\": \"Describe the chart.\"}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifact Toolkit configuration. Navigate to the ReadFile tool Test Settings panel. | Panel opens. List of available parameters displayed. |
| 2 | Locate the `extra_params` field. | Field is visible and editable. |
| 3 | Enter `{"extracted_images_names": ["image1.jpeg"], "read_images_only": true, "prompt": "Describe the chart."}` into `extra_params`. Set `is_capture_image=True`, filename: `docx_with_images.docx`, bucket: `test`. | JSON string is accepted. No validation error shown. |
| 4 | Run the test. | Test executes. Response contains transcription for `image1.jpeg` only. Document text suppressed (`read_images_only=true`). Custom prompt applied. |

## Expected Final State

Test executes. Response contains transcription for `image1.jpeg` only. Document text suppressed (`read_images_only=true`). Custom prompt applied.

## Pass/Fail Criteria

**Pass:**
- `extra_params` field accepts JSON string without error
- Test runs and selective transcription is returned per parameters

**Fail:**
- `extra_params` field missing from UI
- JSON string rejected with validation error
- Test fails or ignores the extra params
