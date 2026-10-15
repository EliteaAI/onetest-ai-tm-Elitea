---
id: ELITEA-3750
title: "DIAL model on a protocol that does not fit its family returns a visible error"
priority: high
type: functional
module: model-settings
status: ready
execution_type: manual
tags: [feat:llm-models, dial, api-protocol, error-handling, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6707"]
---

# ELITEA-3750: DIAL model on a protocol that does not fit its family returns a visible error

**Module:** model-settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that a DIAL model configured with a protocol that does not match its family fails with a clear, visible error, not an empty reply.

---

## Preconditions

- An AI DIAL credential; an agent you can switch between models.

---

## Test Data

| Field | Value |
|-------|-------|
| Misconfigurations | Claude-family on OpenAI; other-family (e.g. Gemini) on OpenAI; other-family on Anthropic; Claude-family on Azure OpenAI with reasoning off |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure a Claude-family DIAL model with the OpenAI protocol and run a plain prompt. | An error is shown to the user, naming the problem (e.g. route/model not supported). |
| 2 | Repeat with an other-family model on OpenAI. | A visible error. |
| 3 | Repeat with an other-family model on Anthropic. | A visible error. |
| 4 | Configure a Claude-family model on Azure OpenAI with reasoning off and run a plain prompt. | Either a correct answer, or a visible error. Record which. |
| 5 | (API) Check the predict response for each failing case. | `error` is set; the response is not an HTTP 200 with an empty answer. |

---

## Expected Final State

Misconfigured protocols never fail silently.

---

## Pass/Fail Criteria

**Pass:**
- Every failing combination shows an error to the user and in the API response.

**Fail:**
- A failing combination returns HTTP 200 with `error: null` and an empty answer (silent failure).
