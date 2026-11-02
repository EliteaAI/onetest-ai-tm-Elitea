---
id: ELITEA-4322
title: "Code Block Download Control Behaves Correctly With Regenerate, Delete, and Edit-and-Regenerate"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- A direct chat conversation exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Give me a short html snippet" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the initial prompt and wait for the AI response containing a code block | Response renders with code block and Download icon |
| 2 | Click "Regenerate" on this response | A new response is generated, replacing the previous one, with its own code block and Download icon |
| 3 | Click Download on the regenerated response's code block | Downloaded file content matches the regenerated code block's content, not the original (pre-regeneration) content |
| 4 | Click "Delete" on the AI response message containing the code block | The message, including its code block and Download icon, is removed from the chat with no console error |
| 5 | Edit the original user message and resend it to trigger a new AI response | A new AI response with a new code block and Download icon appears |
| 6 | Click Download on this new response's code block | File downloads successfully with content matching the new code block, independently scoped from any prior response |
| 7 | Send a new prompt that produces a code block response, and while the response is still streaming (code block partially rendered), attempt to click Download if the icon is visible | Either the Download icon is not yet present/active during streaming, or clicking it after streaming completes produces a complete, non-corrupted file; no partial/corrupted file is produced |

## Expected Final State

The Download control correctly reflects the current state of the message after regenerate, delete, and edit-and-regenerate actions, with no stale, orphaned, or corrupted downloads.

## Pass/Fail Criteria

**Pass:**
- Regenerate updates the Download control to reflect new content
- Delete removes the message and its Download control cleanly
- Edit-and-regenerate produces a new, independently functioning Download control
- No corrupted or partial file is produced from mid-stream interaction

**Fail:**
- Download produces stale content after regeneration
- Download control persists or errors after message deletion
- Downloaded file is corrupted or partial due to streaming state
