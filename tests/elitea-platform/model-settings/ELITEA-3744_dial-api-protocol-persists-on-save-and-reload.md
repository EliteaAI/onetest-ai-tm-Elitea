---
id: ELITEA-3744
title: "DIAL model API protocol persists across save, reload and edit"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, api-protocol, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707", "EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-3744: DIAL model API protocol persists across save, reload and edit

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify the selected API protocol is stored and shown again after reload, and that changing it on an existing model is saved.

---

## Preconditions

- Logged in as a project admin with an AI DIAL credential in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Model | Any DIAL deployment ID |
| Protocols | OpenAI, Azure OpenAI, Anthropic |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a DIAL model with protocol OpenAI and save. | Saved. |
| 2 | Reload the page and open the model. | API protocol shows OpenAI. |
| 3 | Change the protocol to Azure OpenAI and save; reload. | API protocol shows Azure OpenAI. |
| 4 | Change the protocol to Anthropic and save; reload. | API protocol shows Anthropic. |
| 5 | (API) GET the configuration and the project model list. | `api_protocol` matches the last saved value in both. |

---

## Expected Final State

The stored protocol always equals the last saved value in the UI and the API.

---

## Pass/Fail Criteria

**Pass:**
- Every reload shows the last saved protocol; the API returns the same value.

**Fail:**
- The protocol reverts, is lost, or differs between the UI and the API.
