---
id: ELITEA-4320
title: "Re-validate Existing Chat Message Actions After Download Button Addition"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- A chat conversation exists with at least one AI response containing markdown formatting and code blocks
- This is a regression re-check of ELITEA-0502 (Chat Message Actions) and ELITEA-0494 (Verify copied chat messages retain original formatting), triggered by the new Download icon added to the code block toolbar

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Explain Python list comprehension with code examples and a bulleted summary" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat`, open or create a conversation, and send the Test Data prompt | AI responds with a formatted message containing a code block, bullet points, and the new Download icon in the code block toolbar |
| 2 | Re-run ELITEA-0502: click the message-level Copy action on the AI response | Message content is copied to clipboard without error |
| 3 | Paste the copied content into a text editor | Copied content pastes successfully (message-level copy behavior unchanged by the new per-code-block Download icon) |
| 4 | Re-run ELITEA-0502: click "Delete" on the AI response message | Message is removed from the chat with no console error |
| 5 | Send a new message, then re-run ELITEA-0502: click "Clear History" / clear chat action | Chat history is cleared as expected |
| 6 | Send the Test Data prompt again and re-run ELITEA-0494: click the Copy code button on the rendered code block (not the new Download icon) | Code block content is copied to clipboard retaining original formatting (code block structure preserved), unaffected by the adjacent new Download icon |
| 7 | Paste the copied code block content into a text editor | Content matches the original code block formatting, with no stripped or flattened markdown |

## Expected Final State

All pre-existing chat message actions (message copy, delete, clear history, code block copy with formatting retention) continue to function exactly as before the Download icon was introduced, with no regression traceable to the new toolbar control.

## Pass/Fail Criteria

**Pass:**
- Message copy, delete, and clear history all work exactly as in ELITEA-0502
- Code block copy retains original formatting exactly as in ELITEA-0494
- No visual or functional interference between the new Download icon and the pre-existing actions

**Fail:**
- Any of the pre-existing message actions (copy, delete, clear history) is broken, missing, or behaves differently
- Copy code no longer retains formatting, or is confused with/replaced by the new Download action
