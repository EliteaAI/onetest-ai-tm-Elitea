---
id: ELITEA-3574
title: "Out-of-Scope Capabilities Are Not Exposed by the Teams Toolkit"
priority: medium
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3574: Out-of-Scope Capabilities Are Not Exposed by the Teams Toolkit

**Module:** Teams Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Teams toolkit exposes exactly its 7 defined tools and no additional capabilities beyond the documented scope (e.g. no team/channel creation, no message editing/deletion, no meeting scheduling).

## Preconditions

- Access to the Teams toolkit's detail/configuration view and documentation

## Test Data

| Capability | Expected Presence |
|---|---|
| `list_teams`, `list_channels`, `list_chats`, `find_chat_messages`, `search_teams_messages`, `send_chat_message`, `send_channel_message` | Present |
| Create/delete team or channel | Absent |
| Edit or delete an already-sent message | Absent |
| Schedule/manage a meeting | Absent |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Teams toolkit's detail/configuration view | Exactly 7 tools are listed, matching the documented set |
| 2 | Review the toolkit documentation/tool list for any team/channel creation, message edit/delete, or meeting-management capability | None of these out-of-scope capabilities are present as tools |

## Expected Final State

The toolkit's exposed tool set exactly matches the 7 documented tools, with no additional out-of-scope capabilities.

## Pass/Fail Criteria

**Pass:**
- Exactly the 7 documented tools are present; no out-of-scope capability is exposed

**Fail:**
- Any out-of-scope capability (creation, edit/delete of sent messages, meeting management) is present, or a documented tool is missing
