---
id: ELITEA-0951
title: "Project Context Is Injected for Agent Run on Agent Page"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, private-project, feat:settings, team-project, story:3395, r-2.0.4, agents]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0951: Project Context Is Injected for Agent Run on Agent Page

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Project Context is injected when an agent is run directly from the Agent page.

**Coverage:**
- Agent on Agent page receives context with toggle ON
- Works in Private and Team projects
- Context not injected when toggle is OFF

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Green heron dives at twilight`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Green heron dives at twilight'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Navigate to the Agents page. Open an agent and run it from the Agent page (not Chat). Ask: 'What is the QA-TEST-PHRASE?' | Agent returns: 'Green heron dives at twilight'. |
| 3 | Repeat in both Private and Team projects. | Context is injected correctly in both project types. |
| 4 | Set toggle = OFF. Run the agent from the Agent page again with the same question. | Agent does NOT return the phrase. |

## Expected Final State

Agent does NOT return the phrase.

## Pass/Fail Criteria

**Pass:**
- Agent on Agent page returns phrase with toggle ON
- Works in both project types
- No injection with toggle OFF

**Fail:**
- Agent on Agent page does not return phrase with toggle ON
- Context leaks through with toggle OFF
