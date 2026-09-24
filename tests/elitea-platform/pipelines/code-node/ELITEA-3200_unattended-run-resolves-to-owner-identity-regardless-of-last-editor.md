---
id: ELITEA-3200
title: "Unattended Run Resolves to the Pipeline Owner's Identity Regardless of Who Last Edited the Pipeline"
priority: high
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, unattended-runs]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3200: Unattended Run Resolves to the Owner's Identity, Not the Last Editor's

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Functional

**Objective:** When the pipeline/application owner does have a personal project and the requested secret is shared there, an unattended (scheduled/webhook) run must succeed and resolve to the owner's value — even if a different user (e.g. an Editor) was the one who last modified the pipeline.

**Coverage:** TC-CN-06b

## Preconditions

- Pipeline owned by User A (Admin), who has a personal secret `AQA_TOKEN`, shared = ON
- User B (Editor) makes the most recent edit/save to the pipeline (e.g. a cosmetic change) without changing ownership
- Pipeline has a schedule/webhook trigger configured

## Code Node

```python
value = elitea_client.get_private_project_secret('AQA_TOKEN')
test_results = {"value": value, "length": len(value) if value else 0}
print(test_results)
test_results
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the pipeline owner is still User A after User B's edit. | Ownership unchanged. |
| 2 | Trigger the pipeline via schedule/webhook. | Run completes. |
| 3 | Inspect the resolved value. | Value equals User A's (the owner's) `AQA_TOKEN` value — not User B's, even though B made the last edit. |

## Expected Final State

The unattended run's resolved secret always tracks pipeline ownership, never the identity of whoever last saved the pipeline.

## Pass/Fail Criteria

**Pass:**
- Resolved value matches the owner's secret, independent of the last editor

**Fail:**
- Resolved value matches the last editor's secret instead of the owner's
- Run fails despite the owner having a valid, shared secret
