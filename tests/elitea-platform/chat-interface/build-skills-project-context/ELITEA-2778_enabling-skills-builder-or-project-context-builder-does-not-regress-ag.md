---
id: ELITEA-2778
title: "Enabling Skills Builder or Project Context Builder does not regress Agent & Pipeline Builder or Ask User flows"
priority: critical
type: regression
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, regression, agent-pipeline-builder, ask-user]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2778: Enabling Skills Builder or Project Context Builder does not regress Agent & Pipeline Builder or Ask User flows

## Preconditions

- User is logged in to `{{base_url}}`
- A project with an existing Agent and Pipeline exists

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat Modules menu and enable Agent & Pipeline Builder and Ask User only | Both modules show as enabled; Skills Builder and Project Context Builder remain disabled |
| 2 | Request creation of an Agent via chat with an incomplete description | The assistant proceeds with Agent creation and triggers an Ask User clarifying-question card as before |
| 3 | Answer the clarifying question(s) and submit | Agent creation flow resumes and completes successfully |
| 4 | Repeat the same flow requesting Pipeline creation instead of Agent creation | Pipeline creation flow behaves identically to pre-existing behavior, including Ask User clarification |

## Expected Final State

Agent & Pipeline Builder and Ask User continue to function exactly as before the Skills Builder / Project Context Builder modules were introduced.

## Pass/Fail Criteria

**Pass:**
- Agent creation via chat completes after clarification
- Pipeline creation via chat completes after clarification
- No new errors or regressions observed in either flow

**Fail:**
- Agent or Pipeline creation fails, hangs, or behaves differently than before this feature was introduced
- Ask User clarification does not trigger or does not resume the original flow
