---
id: ELITEA-4861
title: "Validate other numeric Admin Features fields after the chat starter limit change"
priority: high
type: regression
module: admin-portal
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The current values of the fields below are noted

## Test Data

| Section → card | Field | Range | Valid value |
|----------------|-------|-------|-------------|
| Skills → Skill Limits | Max Skills Per Agent | 1–200 | 30 |
| Skills → Skill Limits | Max Skill Invocations Per Message | 1–50 | 10 |
| Schedules → Schedule Settings | Minimum Interval | 1–1440 | 15 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For each field in Test Data: enter the valid value, then the minimum, then the maximum | Each value is accepted with no inline error |
| 2 | Enter a value below the minimum and a value above the maximum | No chat-starter "1 to 10" message appears on this field; any error shown uses this field's own range |
| 3 | Click Discard | The field goes back to its original value |
| 4 | Reopen the section | All values are unchanged (nothing was saved) |

## Expected Final State

The other numeric settings are unchanged and unaffected by the chat starter field.

## Pass/Fail Criteria

**Pass:**
- Valid and boundary values are accepted; no "1 to 10" message leaks onto other fields; Discard restores each value

**Fail:**
- A valid or boundary value shows an error, another field shows the chat-starter message, or a value is changed
