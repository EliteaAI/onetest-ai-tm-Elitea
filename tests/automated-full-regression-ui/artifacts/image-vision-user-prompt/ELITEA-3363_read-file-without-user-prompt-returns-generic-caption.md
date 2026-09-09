---
id: ELITEA-3363
title: "read_file Without user_prompt Returns Generic Caption (Backward Compatibility)"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
automation_test_id: 
automation_pr: 
tags: [automated:UI:regression, feat:artifacts, feat:image-vision, r-2.0.6, backward-compatibility]
requirements: [EliteaAI/elitea_issues#6530]
---

# ELITEA-3363: read_file Without user_prompt Returns Generic Caption (Backward Compatibility)

**Module:** artifacts · **Priority:** high · **Type:** regression

**Objective:** Verify that `read_file` for an image file without `extra_params` returns a generic image description/caption, ensuring backward compatibility.

---

## Preconditions

- User is logged in to the Elitea platform
- Agent with Artifact Toolkit is available
- Test image `test_image.png` is uploaded to bucket `attachments`
- Multimodal LLM is configured

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket | attachments |
| Image file | test_image.png |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat with an agent that has Artifact Toolkit | Chat interface loads |
| 2 | Send message: `Read the image test_image.png from bucket attachments and describe what you see` | Agent processes the request |
| 3 | Wait for response | Response is returned within 30 seconds |
| 4 | Verify the agent calls `read_file` without `extra_params` or `user_prompt` | Tool call does not include custom prompt parameter |
| 5 | Verify the response is a generic image description | Response contains a full description of the image content |
| 6 | Verify the description covers multiple aspects of the image | Response describes objects, colors, layout, etc. |
| 7 | Verify no errors in the response | No error messages present |

---

## Expected Final State

The agent returns a comprehensive generic caption describing the full image content, matching pre-enhancement behavior.

---

## Pass/Fail Criteria

**Pass:**
- Generic image caption returned
- Description covers multiple aspects of the image
- No errors occur
- Behavior matches pre-enhancement release

**Fail:**
- Empty or blank response
- Error when `extra_params` not provided
- Breaking change detected
