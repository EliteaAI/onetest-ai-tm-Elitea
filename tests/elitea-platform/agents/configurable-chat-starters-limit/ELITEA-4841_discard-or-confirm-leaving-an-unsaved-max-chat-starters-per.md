---
id: ELITEA-4841
title: "Discard or confirm leaving an unsaved Max Chat Starters per Version change"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin
- The stored Max Chat Starters per Version value is known (written below as `S`, for example 6)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/admin/app/features#chat_configuration` |
| Changed value | `8` (any valid value other than `S`) |
| Another Features section | Skills |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Admin → Features → Chat Configuration and expand Chat Starters without changing anything | Save and Discard are both disabled |
| 2 | Change the value from `S` to `8` | Save and Discard become enabled |
| 3 | Click Discard | The field goes back to `S`; Save and Discard are disabled again |
| 4 | Change the value to `8` again and click another Features section (Skills) | An unsaved-changes confirmation is shown |
| 5 | Cancel the confirmation | You stay on Chat Configuration and the field still shows 8 |
| 6 | Click Skills again and confirm leaving | The Skills section opens |
| 7 | Check the stored value (admin value API or reopen the card) | The value is still `S` |

## Expected Final State

Nothing was saved. The platform limit is still `S`.

## Pass/Fail Criteria

**Pass:**
- Discard reverts the field and disables both buttons
- Leaving with an unsaved change asks for confirmation; Cancel keeps the edit and confirming leaves without saving

**Fail:**
- Discard doesn't revert, or the buttons stay enabled
- Leaving with an unsaved change gives no confirmation, or the unsaved value gets stored
