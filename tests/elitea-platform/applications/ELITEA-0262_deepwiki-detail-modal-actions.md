---
id: ELITEA-0262
title: "DeepWiki Detail Modal: Actions"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0262: DeepWiki Detail Modal: Actions

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all action buttons and close mechanisms in the DeepWiki detail modal work correctly.

**Coverage:**
- "+ Create App" button in modal opens DeepWiki creation form
- "View Configured" button shows configured DeepWiki apps
- X close button and overlay click dismiss the modal

## Preconditions

- Logged in as a project member
- DeepWiki detail modal is open (click Deepwiki chip on the card)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click '+ Create App' inside the open DeepWiki modal | Creation form opens pre-set to DeepWiki type |
| 2 | Navigate back and reopen the DeepWiki modal | Modal opens again |
| 3 | Click 'View Configured' inside the modal | Configured tab opens showing DeepWiki-type apps |
| 4 | Navigate back and reopen the DeepWiki modal | Modal opens again |
| 5 | Click the 'X' button in the top-right corner of the modal | Modal dismisses; Request App page is shown |
| 6 | Reopen the modal; then click the background overlay outside the modal | Modal dismisses |

## Expected Final State

Modal dismisses

## Pass/Fail Criteria

**Pass:**
- All actions navigate correctly
- Modal dismisses on both X click and overlay click

**Fail:**
- Any button navigates incorrectly or modal does not dismiss
