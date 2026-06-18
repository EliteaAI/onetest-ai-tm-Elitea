---
id: ELITEA-0930
title: "Published Agent Respects Project Context Injection and Toggle"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [published-agent, project-context, feat:settings, story:3395, r-2.0.4, agents]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0930: Published Agent Respects Project Context Injection and Toggle

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that published agents in Agent Studio respect Project Context injection and the enable toggle.

**Coverage:**
- Published agent receives context with toggle ON
- Works in Private and Team projects
- Published agent does not receive context with toggle OFF

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Amber light before the storm`
- A published agent in Agent Studio

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Amber light before the storm'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Open a published agent in Agent Studio (Private project). Ask: 'What is the QA-TEST-PHRASE?' | Published agent returns: 'Amber light before the storm'. |
| 3 | Repeat in a Team project with a published agent. | Same result in Team project. |
| 4 | Set Enable toggle = OFF. Run the published agent again. | Published agent does NOT return the phrase. |

## Expected Final State

Published agent does NOT return the phrase.

## Pass/Fail Criteria

**Pass:**
- Published agent returns phrase with toggle ON
- Works in both project types
- No injection with toggle OFF

**Fail:**
- Published agent does not receive context with toggle ON
- Published agent receives context with toggle OFF
