---
id: ELITEA-3364
title: "read_file with user_prompt Works for JPEG Format"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
automation_test_id: 
automation_pr: 
tags: [automated:UI:regression, feat:artifacts, feat:image-vision, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6530]
---

# ELITEA-3364: read_file with user_prompt Works for JPEG Format

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that `read_file` with `user_prompt` works correctly for JPEG images (.jpg extension), not just PNG.

---

## Preconditions

- User is logged in to the Elitea platform
- Agent with Artifact Toolkit is available
- Test image `test_photo.jpg` is uploaded to bucket `attachments` (JPEG format with identifiable content)
- Multimodal LLM is configured

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket | attachments |
| Image file | test_photo.jpg |
| user_prompt | "How many objects are visible in this image?" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat with an agent that has Artifact Toolkit | Chat interface loads |
| 2 | Send message: `Call read_file on test_photo.jpg (attachments bucket) with extra_params={"user_prompt": "How many objects are visible in this image?"}` | Agent processes the request |
| 3 | Wait for response | Response is returned within 30 seconds |
| 4 | Verify the response answers the specific question about count | Response contains a number or count answer |
| 5 | Verify JPEG format is processed correctly | No format-related errors |
| 6 | Verify behavior is consistent with PNG format | Response style matches PNG behavior |

---

## Expected Final State

JPEG image is processed with `user_prompt` and returns a specific answer, same as PNG format.

---

## Pass/Fail Criteria

**Pass:**
- JPEG file processed successfully
- Response answers the specific question
- Behavior consistent with PNG

**Fail:**
- JPEG format fails or errors
- Different behavior between JPEG and PNG
- `user_prompt` ignored for JPEG
