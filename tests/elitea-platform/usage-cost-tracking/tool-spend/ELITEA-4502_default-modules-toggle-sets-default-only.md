---
id: ELITEA-4502
title: "Web Search Default Modules toggle sets only the default state for new chats/agents"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4502: Web Search Default Modules toggle sets only the default state for new chats/agents

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Confirm that the Settings → General → Default Modules "Web Search" toggle (Chats / Agents columns) only controls whether the Web Search feature is pre-enabled by default on a newly created chat or agent, and that a user can still manually turn Web Search on or off for an individual chat/agent regardless of this default.

**Coverage:**
- New chats/agents inherit the current default correctly
- Manual per-chat/per-agent overrides take precedence over the default
- Changing the default never retroactively affects existing chats/agents

## Preconditions

- User has access to Settings → General → Default Modules with the Web Search row

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the "Chats" column default to OFF, start a brand-new chat. | Web Search toggle inside that chat is off by default. |
| 2 | Ask a question requiring a live web search in that chat. | No `web_search` call is triggered (no new entry in Settings → Analytics → Tools tab call count). |
| 3 | In that same chat, manually turn the Web Search toggle ON. | Toggle can be enabled per-chat despite OFF default. |
| 4 | Ask a qualifying question. | `web_search` call is now triggered. |
| 5 | Set the "Chats" column default to ON, start another brand-new chat. | Web Search toggle inside that chat is on by default. |
| 6 | Ask a qualifying question without enabling anything. | `web_search` call is triggered automatically. |
| 7 | In that chat, manually turn Web Search OFF. | Toggle can be disabled per-chat despite ON default. |
| 8 | Ask a qualifying question. | No `web_search` call is triggered. |
| 9 | Repeat steps 1–8 for the "Agents" column (create new agents instead of chats). | Same default/override behavior holds for agents. |
| 10 | Change the Default Modules toggle, then check previously created chats/agents. | Default change does NOT retroactively change the Web Search state of chats/agents created before the change. |

## Expected Final State

The Default Modules toggle only controls the initial state of newly created chats/agents; manual per-chat/per-agent overrides always take precedence, and changing the default never affects existing chats/agents.

## Pass/Fail Criteria

**Pass:**
- New chats/agents inherit the current default correctly
- Manual overrides work regardless of default
- Changing the default never retroactively affects existing chats/agents

**Fail:**
- Default toggle acts as a hard allow/deny gate instead of a default, or retroactively changes existing chats/agents
