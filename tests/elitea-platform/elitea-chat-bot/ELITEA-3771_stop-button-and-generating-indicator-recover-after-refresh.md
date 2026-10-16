---
id: ELITEA-3771
title: "Stop button and generating indicator recover after refresh (event-driven) and display correctly with no delay after chat switch"
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
- Support Assistant widget is available and accessible
## Test Data
| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interruption type | Page refresh / Switch to another chat and back |
| Message content | Any question expected to take several seconds to fully generate |
| Note (refresh) | The FE only updates the Stop button/status indicator in reaction to socket events. A temporary absence immediately after refresh is expected and is not a failure by itself. No fixed response-time threshold is enforced, but the state must recover once the relevant socket event is received while generation is still active. |
| Note (chat switch) | Per retest, the Stop button and "generating" indicator display correctly immediately upon returning to the chat, with no noticeable delay. |
## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant widget and send a message that triggers a multi-second response | Response begins streaming; Stop button and "generating" status indicator are visible |
| 2 | While the response is still generating, refresh the page | Page reloads |
| 3 | Immediately reopen the Support Assistant widget and the same chat | Stop button and "generating" indicator may be temporarily absent right after reopening — this is expected and must not be flagged as a failure on its own |
| 4 | Continue observing (do not refresh again or navigate away) | Once the relevant socket event is received while generation is still active, the Stop button and "generating" indicator reappear. No fixed response-time threshold is enforced |
| 5 | Repeat steps 1-2 with a new message, then switch to a different chat in history and back instead of refreshing | The Stop button and "generating" indicator appear correctly immediately upon returning to the chat, with no noticeable delay |
## Expected Final State
For the refresh scenario, the Stop button/status indicator recover once the relevant socket event is received while generation is still active — no fixed time threshold applies. For the chat-switch scenario, the Stop button/status indicator display correctly with no noticeable delay upon return.
## Pass/Fail Criteria
**Pass:** Refresh — a temporary absence immediately after refresh is not treated as a failure by itself, and the Stop button/status indicator reappear once the relevant socket event is received while generation is still active. Chat switch — the Stop button/status indicator display correctly immediately upon return, with no noticeable delay.
**Fail:** Refresh — the Stop button/status indicator never reappear despite generation still being active and a relevant socket event having been received. Chat switch — the Stop button/status indicator fail to display correctly upon return, or display with a noticeable delay.
