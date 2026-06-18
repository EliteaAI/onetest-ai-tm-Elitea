---
id: ELITEA-0232
title: "LLM Model Override Works from Team Project and Private Project"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0232: LLM Model Override Works from Team Project and Private Project

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the LLM model override feature works correctly when the published agent is accessed from both a team project and a private project.

**Coverage:**
- Override functional in team project context
- Override functional in private project context

## Preconditions

- User has access to at least one team project and one private project at {{base_url}}
- Published agent (agentId=16) is accessible from both contexts

## Test Data

Scenario A: Team project — override model: Anthropic Claude 4.6 Sonnet
Scenario B: Private project — override model: GPT-5.2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the team project, open the published agent in chat, switch model to Anthropic Claude 4.6 Sonnet, send a test message. | Valid response returned, no errors. Toolbar shows Anthropic Claude 4.6 Sonnet. |
| 2 | Navigate to the private project, open the same published agent in chat, switch model to GPT-5.2, send a test message. | Valid response returned, no errors. Toolbar shows GPT-5.2. |
| 3 | Confirm in both scenarios that the toolbar reflects the overridden model name after switching. | Toolbar shows the selected model in each context. |

## Expected Final State

Toolbar shows the selected model in each context.

## Pass/Fail Criteria

**Pass:**
- LLM model override works without errors in both team and private project contexts
- Model name is correctly shown in toolbar for both scenarios

**Fail:**
- Override blocked or errors appear in either project type
- Model name not updated in toolbar
