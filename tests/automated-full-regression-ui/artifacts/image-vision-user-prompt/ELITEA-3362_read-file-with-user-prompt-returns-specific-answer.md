---
id: ELITEA-3362
title: "read_file with user_prompt Returns Specific Answer for Image"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts, feat:image-vision, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6530]
---

# ELITEA-3362: read_file with user_prompt Returns Specific Answer for Image

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that `read_file` with `extra_params={"user_prompt": "..."}` for an image file returns a specific answer to the question, not a generic image caption.

---

## Preconditions

- User is logged in to the Elitea platform
- Agent with Artifact Toolkit is available
- Test image `test_image.png` is uploaded to bucket `attachments` (image with identifiable content, e.g., colored shapes)
- Multimodal LLM is configured

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket | attachments |
| Image file | test_image.png |
| user_prompt | "What is the color of the main object in this image?" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat with an agent that has Artifact Toolkit | Chat interface loads |
| 2 | Send message: `Call read_file on test_image.png (attachments bucket) with extra_params={"user_prompt": "What is the color of the main object in this image?"}` | Agent processes the request |
| 3 | Wait for response | Response is returned within 30 seconds |
| 4 | Verify the response answers the specific question about color | Response contains a color answer (e.g., "green", "red", "blue") |
| 5 | Verify the response is NOT a generic image description | Response does not contain generic description phrases like "The image shows..." followed by full scene description |
| 6 | Verify no errors in the response | No error messages present |

---

## Expected Final State

The agent returns a concise, specific answer to the `user_prompt` question (e.g., "The main object is green" or just "green"), not a generic full description of the image.

---

## Pass/Fail Criteria

**Pass:**
- Response directly answers the specific question
- Response is concise (not a full image description)
- No errors occur

**Fail:**
- Generic image caption returned instead of specific answer
- `user_prompt` parameter ignored
- Error returned
