---
id: ELITEA-2665
title: "Verify file attachment is not allowed during mid-turn input"
priority: medium
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Test file | Any image or document file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a long-running agent turn | Agent begins processing |
| 2 | While agent is running, attempt to click the attachment button | Attachment button is disabled or unavailable |
| 3 | Attempt to drag-and-drop a file | File drop is rejected or disabled |
| 4 | Verify only text input is available | Only text can be entered in input field |

## Expected Final State

File attachments are not allowed during mid-turn input, only plain text as per specification.

## Pass/Fail Criteria

**Pass:**
- Attachment button disabled during agent turn
- Drag-and-drop rejected
- Only plain text accepted

**Fail:**
- Files can be attached mid-turn
- No clear feedback about limitation
