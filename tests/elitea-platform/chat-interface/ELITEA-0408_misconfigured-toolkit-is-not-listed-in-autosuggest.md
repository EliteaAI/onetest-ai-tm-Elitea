---
id: ELITEA-0408
title: "Misconfigured Toolkit Is Not Listed in `/` Autosuggest"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0408: Misconfigured Toolkit Is Not Listed in `/` Autosuggest

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a misconfigured Toolkit added to Participants is silently excluded from the `/` autosuggest and no error message is shown.

**Coverage:**
- Properly configured toolkit appears in autosuggest
- Misconfigured toolkit is excluded silently (no error toast/message)

## Preconditions

- Logged in; two toolkits added to Participants: one properly configured (Artifacts), one misconfigured (invalid credentials/missing required field)

## Test Data

- Toolkit 1: Artifacts — properly configured
- Toolkit 2: misconfigured toolkit (e.g., invalid API key)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open new chat conversation. Add both Artifacts and the misconfigured toolkit to Participants. | Both appear under Toolkits in the Participants panel. |
| 2 | Click the chat input and type /. | Autosuggest dropdown opens. |
| 3 | Inspect the dropdown list. | Only Artifacts appears. The misconfigured toolkit is absent. |
| 4 | Verify no error message, toast, or banner is shown. | The UI shows no additional error indicators related to the excluded toolkit. |

## Expected Final State

The UI shows no additional error indicators related to the excluded toolkit.

## Pass/Fail Criteria

**Pass:**
- Misconfigured toolkit absent from dropdown
- No error message displayed

**Fail:**
- Misconfigured toolkit appears in dropdown
- Error message/toast shown after typing /
