---
id: ELITEA-4047
title: "DIAL API protocol field is shown only for DIAL credentials and is required"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, api-protocol, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707", "EliteaAI/elitea_issues#6713", "EliteaAI/elitea_issues#6919"]
---

# ELITEA-4047: DIAL API protocol field is shown only for DIAL credentials and is required

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify the API protocol field appears only when an AI DIAL credential is selected, offers exactly OpenAI / Azure OpenAI / Anthropic, and must be filled in before a new model can be saved.

---

## Preconditions

- Logged in to {{base_url}} as a project admin.
- The project has at least one AI DIAL credential and at least one non-DIAL AI credential (e.g. OpenAI, Azure OpenAI, Bedrock or Vertex).

---

## Test Data

| Field | Value |
|-------|-------|
| DIAL credential | Any AI DIAL credential in the project |
| Non-DIAL credential | Any non-DIAL AI credential in the project |
| Model Name | Any DIAL deployment ID available to the credential |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → AI Providers → New LLM Model Provider. | The form opens. |
| 2 | Select the non-DIAL credential in AI Credentials. | No API protocol field is shown. |
| 3 | Switch AI Credentials to the DIAL credential. | An API protocol field appears with exactly three options: OpenAI, Azure OpenAI, Anthropic. A tooltip explains which model families use which protocol. |
| 4 | Fill all required fields except API protocol and click Save. | Save is blocked with "API protocol is required.". |
| 5 | Select a protocol and click Save. | The model is saved. |
| 6 | Switch the credential on the saved model to another credential. | The selected protocol is cleared. |

---

## Expected Final State

The protocol field appears only for DIAL credentials and is mandatory for new DIAL models.

---

## Pass/Fail Criteria

**Pass:**
- Field hidden for non-DIAL credentials and shown for DIAL credentials with the three options.
- A new DIAL model cannot be saved without a protocol.

**Fail:**
- Field shown for non-DIAL credentials, missing for DIAL, other options listed, or a DIAL model saves without a protocol.
