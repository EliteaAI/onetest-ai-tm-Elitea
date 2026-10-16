---
id: ELITEA-3773
title: "No stale Stop button or generating indicator shown when reopening a chat with an already-completed response"
priority: critical
type: regression
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, eng:frontend, nfr:usability, rca:missing-functionality, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6280]
---
## Preconditions
- User is logged in to `{{base_url}}`
## Test Data
| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interruption type | Page refresh / Switch to another chat and back |
## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message and wait for the response to fully complete | Response finishes; Stop button and status indicator disappear |
| 2 | Refresh the page | Page reloads |
| 3 | Reopen the same chat | No Stop button or "generating" indicator is shown for the completed message |
| 4 | Send a new message and wait for it to fully complete | Response finishes |
| 5 | Switch to a different chat, then switch back to this chat instead of refreshing | No Stop button or "generating" indicator is shown for the completed message |
## Expected Final State
Completed responses never display an active Stop button or "generating" indicator after a refresh or chat switch.
## Pass/Fail Criteria
**Pass:** No Stop button or status indicator appears for completed messages in either scenario.
**Fail:** A Stop button or "generating" indicator incorrectly appears for a message that has already fully completed.
