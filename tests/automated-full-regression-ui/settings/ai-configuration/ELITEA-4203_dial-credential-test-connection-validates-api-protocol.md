---
id: ELITEA-4203
title: "DIAL credential test connection validates API protocol correctly"
priority: critical
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

## Preconditions

- User is logged in to `{{base_url}}` as a project admin.
- A saved DIAL credential exists in the project.
- A known DIAL model name and its correct API protocol are available for testing.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/ai-providers` |
| DIAL Credential | Existing saved DIAL credential |
| Model Name | Known valid DIAL deployment/model name |
| Correct Protocol | The API protocol that actually works for this model |
| Wrong Protocol | A different protocol that should fail for this model |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Settings → AI Providers → "+ AI Provider" → "LLM model" | New LLM Model Provider form opens. |
| 2 | Select the DIAL credential | API protocol field appears (required for DIAL). |
| 3 | Enter the known valid Model Name | Field accepts input. |
| 4 | Select the wrong protocol for this model | Protocol selected. |
| 5 | Click Test connection | Result returned. |
| 6 | Observe result | Failure result (e.g., "Wrong API protocol or route" or similar error). |
| 7 | Change to the correct protocol | Protocol updated. |
| 8 | Click Test connection again | Result returned. |
| 9 | Observe result | Success result ("Connected in N s"). |

## Expected Final State

Test connection distinguishes wrong vs. correct protocol for the same DIAL model/credential combination. Wrong protocol fails; correct protocol succeeds.

## Pass/Fail Criteria

**Pass:**
- Wrong protocol produces failure result.
- Correct protocol produces success result ("Connected in N s").
- Same credential and model name used in both cases.

**Fail:**
- Either protocol produces the opposite result.
- Test connection does not validate protocol against the model.

## Notes

**Source functional tests:** ELITEA-4164

**Regression rationale:** DIAL credentials require API protocol selection, which is a distinct configuration dimension not present for non-DIAL providers (OpenAI, Azure OpenAI). Wrong protocol is a unique failure mode specific to DIAL. Critical path for DIAL users; must protect against protocol misconfiguration or validation bypass.

**Selected checkpoints:**
- DIAL credential selected → API protocol field appears (required)
- Wrong protocol + valid model → failure
- Correct protocol + same valid model → success
