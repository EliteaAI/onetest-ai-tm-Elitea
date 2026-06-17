---
id: ELITEA-0302
title: "Image Reading Regression – Alternative Multimodal LLM (GPT-4 Vision / Gemini)"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0302: Image Reading Regression – Alternative Multimodal LLM (GPT-4 Vision / Gemini)

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that reading an image from an artifact bucket still works correctly with multimodal LLMs other than Claude (e.g., GPT-4 Vision or Gemini Pro Vision), ensuring the fix for #3644 does not break existing integrations.

**Coverage:**
- readFile on an image via a non-Claude multimodal LLM succeeds
- Image description is returned correctly
- No regressions introduced for non-Claude LLM image processing

## Preconditions

- Logged in to {{base_url}}
- At least one non-Claude multimodal LLM is available in the project (e.g., GPT-4 Vision, Gemini Pro Vision)
- An Artifact Toolkit is configured with a bucket containing an image file

## Test Data

- LLM: GPT-4 Vision or Gemini Pro Vision (any available non-Claude multimodal model)
- Image filename: sample.png
- Bucket: any bucket with sample.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar and open a conversation. | Conversation editor is open. |
| 2 | Add the configured Artifact Toolkit as a participant. | Artifact Toolkit is listed in participants. |
| 3 | Set the LLM to a non-Claude multimodal model (e.g., GPT-4 Vision or Gemini Pro Vision). | The selected non-Claude model is active. |
| 4 | Send: 'Read the image sample.png from the bucket and describe its content.' | Agent invokes readFile tool. |
| 5 | Observe the response. | Agent returns a description of the image without errors. No regressions introduced. |

## Expected Final State

Agent returns a description of the image without errors. No regressions introduced.

## Pass/Fail Criteria

**Pass:**
- Agent reads the image and returns a description using the non-Claude LLM
- No errors are raised

**Fail:**
- Image reading fails with a non-Claude multimodal LLM after the fix
- Error introduced by changes for issues #3644 affects other LLM integrations
