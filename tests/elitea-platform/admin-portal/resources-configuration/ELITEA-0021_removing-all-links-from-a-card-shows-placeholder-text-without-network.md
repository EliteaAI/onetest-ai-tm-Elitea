---
id: ELITEA-0021
title: "Removing All Links From a Card Shows Placeholder Text Without Network Errors [Parametrized: Documentation, Release Notes, Video Library, Tutorials]"
priority: medium
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0021: Removing All Links From a Card Shows Placeholder Text Without Network Errors [Parametrized: Documentation, Release Notes, Video Library, Tutorials]

**Module:** Resources Configuration · **Priority:** Medium · **Type:** Functional

**Objective:** Edge case: verify that removing all links from a card results in a placeholder/empty state display on the user-facing Resources page, without causing crashes or network errors. Parametrized across Documentation, Release Notes, Video Library, and Tutorials.

## Preconditions

Logged in as an ELITEA admin user.
The target card is enabled and has at least one link.
Parameters: Documentation, Release Notes, Video Library, Tutorials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources and open the target card section. | Card configuration is visible with at least one link. |
| 2 | Remove all links from the card one by one. | No links remain in the card configuration. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Open the user-facing Resources page and locate the target card. | The card displays a placeholder text (e.g. empty state message). No links are shown. No error is displayed. |
| 5 | Open the browser Network tab and check for errors. | No network errors (no 4xx or 5xx responses) are produced. |

## Expected Final State

No network errors (no 4xx or 5xx responses) are produced.

## Pass/Fail Criteria

Pass: Card shows placeholder/empty state on Resources page with no network errors when all links are removed.
Fail: Card throws an error, crashes the page, or produces network errors.
