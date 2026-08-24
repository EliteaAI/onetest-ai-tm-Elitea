---
id: ELITEA-0895
title: "Recovery targets the correct chat and does not leak Stop button state to unrelated chats"
priority: high
type: regression
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, eng:frontend, nfr:usability, rca:missing-functionality, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6280]
---
## Preconditions
- User is logged in to `{{base_url}}`
- At least two chats exist in history (Chat A and Chat B)
## Test Data
| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Chat A | Chat with an in-progress generation |
| Chat B | Unrelated chat with no active generation |
## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Chat A, send a message that triggers a longer-running response | Response begins streaming in Chat A |
| 2 | While Chat A's response is still generating, switch to Chat B | Chat B is displayed |
| 3 | Observe Chat B for a Stop button or "generating" indicator | Chat B shows no Stop button or "generating" indicator |
| 4 | Switch back to Chat A | Chat A shows the Stop button/status indicator correctly, with no noticeable delay, if generation is still ongoing |
## Expected Final State
Recovery state (Stop button, status indicator) is correctly scoped to the chat with the actual in-progress generation and never appears in unrelated chats.
## Pass/Fail Criteria
**Pass:** Chat B never shows a Stop button/indicator; Chat A shows it correctly with no noticeable delay once returned to.
**Fail:** Chat B incorrectly shows a Stop button/indicator, or Chat A fails to show it (or shows a noticeable delay) when generation is still ongoing.
