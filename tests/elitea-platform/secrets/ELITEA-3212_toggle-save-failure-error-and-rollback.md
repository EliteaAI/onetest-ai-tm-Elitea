---
id: ELITEA-3212
title: "Share Toggle Shows an Error and Rolls Back Its Visual State When the Save Fails"
priority: high
type: negative
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui, error-handling]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3212: Toggle Error/Rollback on Failed Save

**Module:** Secrets · **Priority:** High · **Type:** Negative

**Objective:** Confirm that if the backend rejects or fails a share-toggle change (network error, permission denial, server error), the UI surfaces a clear error and reverts the toggle's visual state to match the actual persisted value — it must never show a toggle state that doesn't match reality.

**Coverage:** TC-UI (error states when toggling fails)

## Preconditions

- A personal secret exists with a known share state
- Ability to simulate a failed request (e.g. devtools network throttling/blocking, or a backend permission change that causes the toggle request to be rejected)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the secret's current toggle state and confirm it matches the backend value. | Confirmed in sync. |
| 2 | Block/fail the toggle's network request (e.g. via devtools request blocking) and then flip the toggle in the UI. | UI shows an error/failure indicator (toast, inline message, or similar). |
| 3 | Inspect the toggle's visual state after the failed attempt. | Toggle has reverted to the last known-good (actual persisted) state — not left showing the attempted new state. |
| 4 | Re-verify against the backend value. | UI state matches backend state exactly after the failure. |
| 5 | Remove the network block and retry the toggle normally. | Toggle now succeeds and persists correctly. |

## Expected Final State

A failed toggle save never leaves the UI showing a state that diverges from the actual persisted value.

## Pass/Fail Criteria

**Pass:**
- Failed save surfaces a clear error and the toggle visually reverts to match the true backend state

**Fail:**
- Toggle visually shows the attempted (unsaved) state after a failure, misleading the user about the secret's actual share status
- No error is shown at all on failure
