---
id: ELITEA-2952
title: "Verify empty messages cannot be queued"
priority: medium
type: functional
module: interjections
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6, interjection, validation, edge-case]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Agent/LLM run active

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Whitespace | "   " (spaces only) |
| Tabs | Tab characters only |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start agent/LLM run | Run begins |
| 2 | Leave composer empty, click Send button | Button disabled, cannot click |
| 3 | Leave composer empty, press Enter | Nothing happens |
| 4 | Type only spaces, attempt to send | Button disabled or message rejected |
| 5 | Type only tabs/newlines, attempt to send | Button disabled or message rejected |
| 6 | Type message then delete all characters | Button returns to disabled state |
| 7 | Verify queue | No empty messages in queue |

## Expected Final State

- No empty or whitespace-only messages in queue
- Send button properly reflects content state

## Pass/Fail Criteria

**Pass:**
- Empty composer → Send disabled
- Whitespace only → Send disabled or rejected
- No empty messages queued

**Fail:**
- Empty messages can be sent
- Whitespace-only messages queued
- Button enabled with empty composer
