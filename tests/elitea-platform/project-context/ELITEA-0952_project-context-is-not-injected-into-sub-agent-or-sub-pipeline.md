---
id: ELITEA-0952
title: "Project Context Is Not Injected into Sub-Agent or Sub-Pipeline"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, story:3395, sub-agent, pipeline, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0952: Project Context Is Not Injected into Sub-Agent or Sub-Pipeline

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Project Context is injected only for the master agent and not passed to any sub-agent or sub-pipeline it calls.

**Coverage:**
- Master agent receives context; sub-agent does not
- Verified from Agent page and Chat page
- Sub-pipeline also does not receive context

## Preconditions

- A master agent configured to call a sub-agent exists
- The master agent's system prompt instructs it to ask its sub-agent: 'What is the QA-TEST-PHRASE?' and relay the sub-agent's exact response back

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Azure falcon rests at midnight`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Azure falcon rests at midnight'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Open the master agent on the Agent page. Send: 'Ask your sub-agent about the QA-TEST-PHRASE and tell me what it said.' | Master agent triggers the sub-agent. |
| 3 | Observe the master agent's response. | Master agent reports that the sub-agent responded it does NOT know the phrase 'Azure falcon rests at midnight' — sub-agent received no context. |
| 4 | Add the master agent as a participant on the Chat page. Send the same question from chat. | Same result — sub-agent is unaware of the phrase in both Agent page and Chat page. |
| 5 | Configure the master agent to call a sub-pipeline instead of a sub-agent. Ask the master to query the sub-pipeline about the QA-TEST-PHRASE. | Master reports the sub-pipeline also does not know the phrase. Context isolation applies to sub-pipelines too. |

## Expected Final State

Master reports the sub-pipeline also does not know the phrase. Context isolation applies to sub-pipelines too.

## Pass/Fail Criteria

**Pass:**
- Master agent knows the phrase
- Sub-agent reports it does not know the phrase
- Sub-pipeline reports it does not know the phrase
- Isolation holds from both Agent page and Chat page

**Fail:**
- Sub-agent or sub-pipeline returns the phrase (isolation broken)
