---
id: ELITEA-3774
title: "Normal uninterrupted Stop click during active streaming cancels generation correctly"
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
| Message content | Any message triggering a multi-second streaming response |
## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message that triggers a multi-second streaming response | Response begins streaming; Stop button visible |
| 2 | Without refreshing or switching chats, click Stop while the response is actively streaming | Generation stops immediately; no further content is appended |
## Expected Final State
Clicking Stop during a normal, uninterrupted streaming session halts generation immediately.
## Pass/Fail Criteria
**Pass:** Generation stops immediately with no further content added after clicking Stop.
**Fail:** Generation continues after clicking Stop, or the button has no effect.
