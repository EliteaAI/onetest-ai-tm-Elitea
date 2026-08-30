---
id: ELITEA-2946
title: "Verify attachments blocked during active agent/LLM run"
priority: critical
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, attachment, bug-6448]
requirements: [EliteaAI/elitea_issues#6115, EliteaAI/elitea_issues#6448]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Feature enabled at platform and project level
- Test files available for upload attempts

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test File | Any image or document file |
| Test Image | Screenshot or PNG for paste test |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run with a task message | Agent/LLM begins processing |
| 2 | Attempt to click attachment button in composer | Attachment button is disabled or hidden |
| 3 | Attempt drag-and-drop file into composer area | File is blocked or ignored, no attachment added |
| 4 | Copy image to clipboard and attempt paste (Ctrl+V) | Paste is blocked or ignored |
| 5 | Type plain text and send as interjection | Message queued without any attachment |
| 6 | Send second plain text interjection | Second message queued without attachment |
| 7 | Wait for run to complete, verify attachment button | Attachment button re-enabled when no run active |

## Expected Final State

- No attachments on any queued messages
- Attachment functionality restored after run completes
- All interjections are plain text only

## Pass/Fail Criteria

**Pass:**
- Attachment button disabled/hidden during active run
- Drag-and-drop blocked
- Paste blocked
- No files attached to queued messages
- Normal attachment works when run completes

**Fail:**
- Attachment button clickable during run
- Files can be attached to interjections
- Attachments persist across queued messages
