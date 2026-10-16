---
id: ELITEA-4055
title: "Changing a DIAL model's protocol or reasoning applies immediately without a LiteLLM sync"
priority: medium
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, api-protocol, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707"]
---

# ELITEA-4055: Changing a DIAL model's protocol or reasoning applies immediately without a LiteLLM sync

**Module:** model-settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a change to the API protocol or the Reasoning toggle takes effect on the next call, without triggering a LiteLLM sync.

---

## Preconditions

- An AI DIAL credential; a DIAL model used by an agent.

---

## Test Data

| Field | Value |
|-------|-------|
| Change | Protocol from Azure OpenAI to the family's recommended protocol; then Reasoning off → on |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the agent once on the current settings. | It answers. |
| 2 | Change the protocol to the recommended one and save. Do not run a LiteLLM sync. | Saved. |
| 3 | Run the agent again. | It answers using the new route (where visible: the new LiteLLM model group / route in logs). |
| 4 | Toggle Reasoning and save, then run again. | The new reasoning setting is applied on this call. |

---

## Expected Final State

Settings changes are live on the next call.

---

## Pass/Fail Criteria

**Pass:**
- The next call after each change uses the new settings.

**Fail:**
- The old route or reasoning setting is still used until a sync.
