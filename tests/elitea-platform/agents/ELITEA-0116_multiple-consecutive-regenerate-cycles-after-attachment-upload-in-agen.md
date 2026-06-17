---
id: ELITEA-0116
title: "Multiple Consecutive Regenerate Cycles After Attachment Upload in Agents"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:attachments, feat:agents]
requirements: [ProjectAlita/projectalita.github.io#3591]
---
# ELITEA-0116: Multiple Consecutive Regenerate Cycles After Attachment Upload in Agents

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking the Regenerate button multiple consecutive times in the Agents section continues to produce new responses after a file was attached — with no degradation, freeze, or silent repeat after repeated cycles.

**Coverage:**
- Three consecutive regeneration cycles after image attachment in agent chat
- Each regeneration cycle re-uses the original message with attachment
- Session state stability across multiple consecutive regenerations
- Regenerate button remains functional throughout all cycles

## Preconditions

- User is logged in to {{base_url}} — Private project active
- An agent is configured with "Allow attachments" toggle enabled and an Artifact bucket assigned
- A JPEG image file prepared (< 5 MB)

## Test Data

- 1× JPEG image (< 5 MB)
- Text prompt: "Describe this image"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section and open the configured agent (Allow attachments enabled, Artifact bucket assigned). | Agent chat interface is open. |
| 2 | Click the paperclip (📎) icon and attach 1 JPEG image (< 5 MB). | Image appears as an attachment chip in the message input area. |
| 3 | Type "Describe this image" and click Send. | Agent produces a first response analyzing the image (1st generation). |
| 4 | Click the Regenerate (🔄) icon near the last agent message. Wait for the full response to complete. | Loading indicator appears and a second complete response is produced (2nd generation). |
| 5 | Click the Regenerate (🔄) icon again. Wait for the full response to complete. | Loading indicator appears and a third complete response is produced (3rd generation). |
| 6 | Click the Regenerate (🔄) icon a third time. Wait for the full response to complete. | Loading indicator appears and a fourth complete response is produced (4th generation). No error, freeze, or crash occurs. |

## Expected Final State

Loading indicator appears and a fourth complete response is produced (4th generation). No error, freeze, or crash occurs.

## Pass/Fail Criteria

**Pass:**
- All three regeneration cycles complete successfully
- Each cycle produces a response with a visible loading indicator
- No error message, freeze, or crash occurs at any cycle
- Regenerate button remains visible and functional after each cycle

**Fail:**
- Any regeneration cycle fails to trigger a new generation
- A cycle returns the same static response silently with no loading indicator
- An error message appears at any cycle
- The UI freezes or crashes during any regeneration
