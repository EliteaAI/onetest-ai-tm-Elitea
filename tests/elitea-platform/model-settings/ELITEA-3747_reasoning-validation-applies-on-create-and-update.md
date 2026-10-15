---
id: ELITEA-3747
title: "Reasoning validation applies the same on create and on update"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, reasoning, validation, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-3747: Reasoning validation applies the same on create and on update

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that reasoning settings are validated identically when a model is created and when it is updated, and that a family which does not support reasoning cannot get it enabled through an update.

---

## Preconditions

- A project admin; API access with a personal token.

---

## Test Data

| Field | Value |
|-------|-------|
| Non-reasoning model | A model whose name is recognized as a family without reasoning support (e.g. a GPT-4-family model) |
| Invalid reasoning data | `default_effort` that is not in `supported_efforts` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create the non-reasoning model with Supports Reasoning off. | Saved. |
| 2 | Update the same model, setting `supports_reasoning=true`. | Rejected with a validation error saying the family does not support reasoning. |
| 3 | Try to create a new model of that family with `supports_reasoning=true`. | Rejected with the same error. |
| 4 | Update a reasoning-capable model with a `default_effort` outside `supported_efforts`. | Rejected, the same way as on create. |

---

## Expected Final State

Create and update enforce the same reasoning rules.

---

## Pass/Fail Criteria

**Pass:**
- Every invalid combination is rejected on both create and update with the same message.

**Fail:**
- Update accepts a combination that create rejects (or the reverse).
