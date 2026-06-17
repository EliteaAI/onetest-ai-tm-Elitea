---
id: ELITEA-0987
title: "[Secrets] Clicking Create from Page 2 Does Not Switch Sort to Creation-Date Order"
priority: high
type: functional
module: secrets
status: ready
execution_type: manual
tags: [feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4866]
---
# ELITEA-0987: [Secrets] Clicking Create from Page 2 Does Not Switch Sort to Creation-Date Order

**Module:** Secrets · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Create while on page 2 (or any non-first page) does not trigger a sort change from alphabetical to creation-date ordering.

**Coverage:**
- Create action initiated from page 2
- Page redirect to page 1 to show creation row is acceptable
- Existing rows must remain A→Z after redirect
- After save, list stays A→Z

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Enough secrets to have at least 2 pages in the list
- Browser: Chrome latest

## Test Data

- New secret name: MidAlpha
- New secret value: mid-value-001

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Secrets and go to page 2 of the list. | Page 2 loads. Items are sorted A→Z. |
| 2 | Click Create / + button. | Page may redirect to page 1 to display the creation row at the top — this is acceptable. Existing rows must remain sorted A→Z and must NOT switch to creation-date ordering. |
| 3 | Fill in name MidAlpha and value mid-value-001, then save. | Secret is created. Creation row disappears from the top. |
| 4 | Observe the list order after creation. | List is sorted A→Z. MidAlpha appears at its correct alphabetical position. |

## Expected Final State

List is sorted A→Z. MidAlpha appears at its correct alphabetical position.

## Pass/Fail Criteria

**Pass:**
- Sort stays A→Z throughout; no switch to creation-date ordering at any stage
- MidAlpha appears at its correct alphabetical position after creation

**Fail:**
- Sort switches to creation-date (old→new or new→old) when clicking Create from page 2
- Existing rows reorder during the creation flow
