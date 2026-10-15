---
id: ELITEA-3748
title: "Non-DIAL credential with reasoning saves without an API protocol error"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, reasoning, validation, bedrock, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6713"]
---

# ELITEA-3748: Non-DIAL credential with reasoning saves without an API protocol error

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that a model on a non-DIAL credential (e.g. Bedrock) can be saved with Supports Reasoning on, on both create and update, without any `api_protocol` validation error.

---

## Preconditions

- A project admin; a Bedrock-type (or other non-DIAL) AI credential in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential | A Bedrock-type credential |
| Model | Any reasoning-capable model available to it |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a model on the Bedrock credential with Supports Reasoning on and save. | Saved; no "api_protocol='azure' does not support reasoning" error; no API protocol field is shown. |
| 2 | Create another model on the same credential with Supports Reasoning off, save, then edit it to turn reasoning on and save. | Saved, with the same behaviour as create. |
| 3 | Run an agent on the model. | It answers. |

---

## Expected Final State

Reasoning on non-DIAL credentials is not blocked by DIAL protocol rules.

---

## Pass/Fail Criteria

**Pass:**
- Both create and update save successfully and the model answers.

**Fail:**
- Any protocol-related validation error on a non-DIAL credential.
