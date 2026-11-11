---
id: ELITEA-4657
title: "Test Connection result reflects the latest form state, not a stale in-flight request, when Model Name and DIAL API Protocol are both changed while a prior test is still pending"
priority: high
type: functional
module: ai-configuration
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6793]
---

# ELITEA-4657: Test Connection Result Race — Latest Field State Must Win

## Preconditions

- A saved DIAL credential exists in the project with at least two valid API protocols (Protocol A, Protocol B) and two distinct valid Model Names (Model 1, Model 2) available, such that both protocol/model combinations are independently testable
- A way to observe or induce a slow/pending Test Connection response (e.g. network throttling or an endpoint with observable latency)

## Test Data

| Field | Value |
|-------|-------|
| API Protocol A | First valid DIAL API protocol |
| API Protocol B | Second valid DIAL API protocol |
| Model 1 | First valid Model Name for Protocol A |
| Model 2 | Second valid Model Name for Protocol B |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the LLM model form, select the DIAL credential, set API Protocol to Protocol A and Model Name to Model 1, click Test Connection | Request starts; button shows in-progress spinner |
| 2 | While the spinner for the Protocol A + Model 1 request is still showing, change Model Name to Model 2 and change API Protocol to Protocol B, without clicking Test Connection again | Fields update; no new request is manually triggered |
| 3 | Observe the Model Name field's "Recognized"/"Not recognized" indicator for Model 2 | Indicator updates correctly for Model 2 before the pending request resolves |
| 4 | Wait for the original in-flight request to resolve | A result is eventually displayed |
| 5 | Inspect the displayed result | Result corresponds to Protocol B + Model 2 (the latest field state), not to the originally requested Protocol A + Model 1 combination |
| 6 | Check for any intermediate flash of a Protocol A + Model 1 result before the final result settles | No stale result is left on screen; the Recognized indicator from step 3 never contradicts the final displayed result |
| 7 | Click Test Connection explicitly once more with the current Protocol B + Model 2 values | Result matches what was displayed in step 5, confirming consistency |

## Expected Final State

Changing Model Name and API Protocol while a Test Connection request is still pending never results in a stale, mismatched result being shown — the UI either discards the stale response or the displayed result is independently correct for the latest field state, and the field-level Recognized indicator stays consistent with it throughout.

## Pass/Fail Criteria

**Pass:**
- The Recognized indicator updates to the new Model Name before the pending request resolves
- The eventual displayed result corresponds only to the latest (Protocol B + Model 2) field state
- No stale result from the superseded request is ever shown, even momentarily

**Fail:**
- The displayed result reflects the original (Protocol A + Model 1) request instead of the latest field state
- A stale result flashes on screen before the correct one appears
- The Recognized indicator and the final Test Connection result disagree with each other
