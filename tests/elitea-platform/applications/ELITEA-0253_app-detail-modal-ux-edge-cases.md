---
id: ELITEA-0253
title: "App Detail Modal: UX Edge Cases"
priority: medium
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0253: App Detail Modal: UX Edge Cases

**Module:** Applications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify modal interaction edge cases: single modal at a time, Escape key, small screen clipping, and read-only capability chips.

**Coverage:**
- Only one modal open at a time
- Escape key closes modal
- Modal not clipped on smaller screens
- Capability chips are read-only

## Preconditions

- Logged in as a project member
- On the Request App tab

## Test Data

Browser resized to 1024×768 for small screen test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the DeepWiki modal; then attempt to trigger the Inventory modal (click Inventory chip) | Only one modal is shown at a time; modals do not stack |
| 2 | With the DeepWiki modal open, press the Escape key | Modal is dismissed |
| 3 | Resize the browser to 1024×768; open either modal | Full modal content is visible and not clipped |
| 4 | Click on a capability chip inside the modal (e.g., 'Repository wiki generation') | Chip is not interactive; no navigation or action is triggered |

## Expected Final State

Chip is not interactive; no navigation or action is triggered

## Pass/Fail Criteria

**Pass:**
- Single modal enforced; Escape dismisses; content not clipped; chips read-only

**Fail:**
- Modals stack, Escape fails, content clipped on small screens, or chips trigger actions
