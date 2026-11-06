---
id: ELITEA-3362
title: "read_file with user_prompt Returns Specific Answer for Image (PNG and JPEG)"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts, feat:image-vision, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6530]
---

# ELITEA-3362: read_file with user_prompt Returns Specific Answer for Image (PNG and JPEG)

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that `read_file` with `extra_params={"user_prompt": "..."}` for an image file returns a specific answer to the question, not a generic image caption — for both PNG and JPEG image formats.

---

## Preconditions

- User is logged in to the Elitea platform
- Agent with Artifact Toolkit is available
- Test image `test_image.png` is uploaded to bucket `attachments` (image with identifiable content, e.g., colored shapes)
- Test image `test_photo.jpg` is uploaded to bucket `attachments` (JPEG format with identifiable content)
- Multimodal LLM is configured

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket | attachments |
| PNG image file | test_image.png |
| PNG user_prompt | "What is the color of the main object in this image?" |
| JPEG image file | test_photo.jpg |
| JPEG user_prompt | "How many objects are visible in this image?" |

---

## Steps

### Part 1: PNG Format

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat with an agent that has Artifact Toolkit | Chat interface loads |
| 2 | Send message: `Call read_file on test_image.png (attachments bucket) with extra_params={"user_prompt": "What is the color of the main object in this image?"}` | Agent processes the request |
| 3 | Wait for response | Response is returned within 30 seconds |
| 4 | Verify the response answers the specific question about color | Response contains a color answer (e.g., "green", "red", "blue") |
| 5 | Verify the response is NOT a generic image description | Response does not contain generic description phrases like "The image shows..." followed by full scene description |
| 6 | Verify no errors in the response | No error messages present |

### Part 2: JPEG Format

| # | Action | Expected Result |
|---|--------|-----------------|
| 7 | Open chat with an agent that has Artifact Toolkit | Chat interface loads |
| 8 | Send message: `Call read_file on test_photo.jpg (attachments bucket) with extra_params={"user_prompt": "How many objects are visible in this image?"}` | Agent processes the request |
| 9 | Wait for response | Response is returned within 30 seconds |
| 10 | Verify the response answers the specific question about count | Response contains a number or count answer |
| 11 | Verify JPEG format is processed correctly with no format-related errors | No format-related errors |
| 12 | Verify behavior is consistent with the PNG case in Part 1 | Response style matches PNG behavior |

---

## Expected Final State

For both PNG and JPEG images, the agent returns a concise, specific answer to the `user_prompt` question, not a generic full description of the image. JPEG is processed without format-related errors and behaves consistently with PNG.

---

## Pass/Fail Criteria

**Pass:**
- For both formats: response directly answers the specific question, is concise (not a full image description), and no errors occur.

**Fail:**
- Generic image caption returned instead of specific answer, for either format.
- `user_prompt` parameter ignored, for either format.
- JPEG format fails or errors, or behaves inconsistently with PNG.
- Error returned.

---

## Notes

**Source functional tests:** ELITEA-3362, ELITEA-3364

**Regression rationale:** ELITEA-3364 is a format variation of ELITEA-3362 (same user_prompt mechanic, different image format/question) rather than a distinct behavior; consolidating avoids duplicating the chat-interaction setup while preserving the PNG and JPEG format checkpoints.

**Selected checkpoints:**
- `user_prompt` returns specific answer for PNG (ELITEA-3362)
- `user_prompt` returns specific answer for JPEG, consistent with PNG (ELITEA-3364)
