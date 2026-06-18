---
id: ELITEA-0986
title: "[Secrets] Sort Order Stays A→Z During and After Secret Creation"
priority: critical
type: functional
module: secrets
status: ready
execution_type: manual
tags: [feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4866]
---
# ELITEA-0986: [Secrets] Sort Order Stays A→Z During and After Secret Creation

**Module:** Secrets · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Secrets list sort order does not change at any point during the creation flow — before, while the creation row is pinned, and after saving.

**Coverage:**
- New creation row pins at top of the list during creation (expected behavior after fix)
- Existing secrets below the new row remain sorted A→Z during creation
- After save completes, new secret lands at correct alphabetical position
- No switch to creation-date ordering at any stage

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- At least 5 secrets exist with names spread across the alphabet (e.g., Apple, Banana, Cherry, Delta, Echo)
- Secrets list is on page 1, sorted A→Z
- Browser: Chrome latest

## Test Data

- New secret name: Cinnamon (alphabetically between Cherry and Delta)
- New secret value: test-value-001

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Secrets. | Secrets list loads. Items are sorted A→Z alphabetically. |
| 2 | Click Create / + button. | New creation row appears pinned at the top of the list. All existing secrets below it remain sorted A→Z — they do not reorder to creation-date. |
| 3 | Fill in the secret name Cinnamon and value test-value-001. | Fields populated. Existing rows below remain A→Z. |
| 4 | Save / confirm the new secret. | Secret is created. The pinned creation row disappears from the top. |
| 5 | Observe the list order after creation completes. | List is sorted A→Z with no creation row pinned. Cinnamon appears at its correct alphabetical position between Cherry and Delta. |

## Expected Final State

List is sorted A→Z with no creation row pinned. Cinnamon appears at its correct alphabetical position between Cherry and Delta.

## Pass/Fail Criteria

**Pass:**
- New row pins at top during creation
- Existing rows stay A→Z throughout
- After save, Cinnamon appears in correct alphabetical slot

**Fail:**
- Existing rows reorder to creation-date during creation
- Cinnamon does not appear at correct alphabetical position after save
