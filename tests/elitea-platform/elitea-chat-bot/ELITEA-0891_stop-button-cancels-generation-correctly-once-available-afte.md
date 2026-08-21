---
id: ELITEA-0891
title: "Stop button cancels generation correctly once available after recovery from refresh or chat switch"
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
- A response is currently generating in the Support Assistant
## Test Data
| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Interruption type | Page refresh / Switch to another chat and back |
| Note | Refresh recovery is event-driven; no fixed response-time threshold is enforced, but the Stop button must become available once the relevant socket event is received while generation is still active. Chat-switch recovery displays with no noticeable delay. |
## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message that triggers a multi-second response | Response begins streaming |
| 2 | While generating, refresh the page | Page reloads |
| 3 | Wait until the Stop button reappears (a temporary absence beforehand is expected, not a failure) | Stop button becomes visible once the relevant socket event is received while generation is still active, with no fixed time threshold enforced |
| 4 | Click the Stop button once it reappears | Generation stops; no further content is appended to the message |
| 5 | Repeat steps 1-2, this time switching to another chat and back instead of refreshing | Stop button is visible correctly immediately upon return, with no noticeable delay |
| 6 | Click the Stop button | Generation stops; no further content is appended to the message |
## Expected Final State
Once the Stop button becomes available — via event-driven recovery after refresh, or immediately after a chat switch — clicking it reliably cancels the in-progress generation.
## Pass/Fail Criteria
**Pass:** In both scenarios, once the Stop button is available, clicking it halts generation with no further content added.
**Fail:** After the Stop button is available, clicking it has no effect and generation continues/completes in the background.
