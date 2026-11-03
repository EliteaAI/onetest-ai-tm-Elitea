---
id: ELITEA-4389
title: "Extremely Large Code Block Download Does Not Degrade Chat Responsiveness"
priority: medium
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
- User has access to a Private project with at least one other existing conversation to switch to
- This case focuses specifically on chat UI responsiveness during/after the download action, distinct from ELITEA-4326's content-integrity check for large blocks

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt (very large code block) | "Give me an extremely long json array with at least 10,000 lines of sample data, as one code block" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open a direct chat conversation | Chat page loads |
| 2 | Send the Test Data prompt and wait for the full response to render | AI responds with a very large fenced code block; the chat UI remains scrollable and responsive while the large block renders |
| 3 | Click the Download icon on the large code block | The download is initiated |
| 4 | While the download is in progress (and immediately after it completes), attempt to scroll the chat conversation | Scrolling remains smooth with no visible freeze, stutter, or multi-second delay attributable to the download |
| 5 | While the download is in progress (and immediately after), type a new message into the chat input field | Typing is responsive with no input lag or dropped keystrokes |
| 6 | Immediately after triggering the download, switch to a different existing conversation in the sidebar | The conversation switch completes normally with no hang, spinner stuck indefinitely, or crash |
| 7 | Return to the original conversation and confirm the large code block and its Download control are still intact and functional | The code block renders correctly and the Download icon remains clickable and functional |
| 8 | Check the browser console for errors or long-task warnings correlated with the download action | No new console errors are introduced by the download action on a large block |

## Expected Final State

The chat UI remains responsive (scrolling, typing, switching conversations) during and immediately after downloading an extremely large code block, with no freeze, crash, or lingering performance degradation, and the code block/Download control remain functional afterward.

## Pass/Fail Criteria

**Pass:**
- Chat scrolling, message typing, and conversation switching all remain responsive during and after the large-block download
- No freeze, crash, or stuck UI state occurs
- No new console errors appear as a result of the download action
- The Download control remains functional after the operation completes

**Fail:**
- The chat UI freezes, lags noticeably, or becomes unresponsive during or after the download
- Switching conversations or typing is blocked or significantly delayed because of the download
- The browser tab crashes or the Download control becomes non-functional afterward
