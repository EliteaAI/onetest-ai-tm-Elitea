---
id: ELITEA-3745
title: "DIAL models answer on the recommended protocol for each model family"
priority: critical
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, api-protocol, agents, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707", "EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-3745: DIAL models answer on the recommended protocol for each model family

**Module:** model-settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a DIAL model from each family answers correctly in an agent when configured with its recommended protocol: GPT-family → OpenAI, Claude-family → Anthropic, Gemini and other families → Azure OpenAI.

---

## Preconditions

- An AI DIAL credential in the project.
- Three DIAL model configurations: one GPT-family on OpenAI, one Claude-family on Anthropic, one from another family (e.g. Gemini) on Azure OpenAI.
- An agent with an artifact toolkit (list / read / create file tools).

---

## Test Data

| Field | Value |
|-------|-------|
| Prompt 1 | A plain question that needs no tools (e.g. a small arithmetic question) |
| Prompt 2 | "Run a quick read-and-create tool smoke test." (needs a list/read and a create tool call) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set the agent's model to the GPT-family DIAL model and send Prompt 1. | A correct answer is returned. |
| 2 | Send Prompt 2. | The agent calls a read/list tool and a create tool and reports success. |
| 3 | Repeat steps 1-2 with the Claude-family DIAL model. | Same result. |
| 4 | Repeat steps 1-2 with the other-family DIAL model. | Same result. |
| 5 | Repeat the Claude-family check with a model id in each available style (e.g. a `claude-…@…` id and an `anthropic.claude-…` id), if both exist. | Both answer. |

---

## Expected Final State

Every model family answers and uses tools on its recommended protocol.

---

## Pass/Fail Criteria

**Pass:**
- All families answer both prompts, with tool calls where requested.

**Fail:**
- Any family returns an error, an empty reply, or no tool calls on its recommended protocol.
