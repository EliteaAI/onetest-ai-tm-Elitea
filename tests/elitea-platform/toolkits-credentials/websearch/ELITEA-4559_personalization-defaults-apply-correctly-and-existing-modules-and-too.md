---
id: ELITEA-4559
title: "Personalization defaults apply correctly and existing modules and toolkits remain unaffected"
priority: high
type: regression
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Project-admin access to Settings → General → Default Modules
- A chat/agent with a pre-existing, manually configured Tavily-based MCP or toolkit (not the new shared mechanism)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |
| Default Modules rows to re-check | Image Creation, Data Analysis, Agent & Pipeline Builder, Skill Builder, Project Context Builder, Ask User, Planner, Python Sandbox, Swarm Mode, Smart Tools Selection |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Default Modules, toggle Web Search "Chats" default ON; create a new chat | Web Search is ON by default in the new chat's Modules |
| 2 | Toggle Web Search "Agents" default ON; create a new agent | New agent's Modules section shows Web Search ON by default |
| 3 | Set both defaults OFF; create another new chat and new agent | Both start with Web Search OFF |
| 4 | Check existing chats/agents created before this change | Their own previously-set Web Search state is unchanged by the new defaults |
| 5 | Toggle and verify persistence for each other Default Modules row listed in Test Data | Every other row still toggles and persists correctly |
| 6 | Open the chat/agent with the pre-existing manual Tavily-based toolkit and run it | It still executes its web-search tools successfully, unaffected by the new Web Search module |

## Expected Final State

New entities correctly inherit the configured defaults; existing entities and unrelated modules/toolkits are unaffected.

## Pass/Fail Criteria

**Pass:**
- Defaults apply only to newly created entities; all other Default Modules rows and the pre-existing manual toolkit continue to work correctly

**Fail:**
- Defaults retroactively change existing entities, or any other module row or the manual toolkit stops working
