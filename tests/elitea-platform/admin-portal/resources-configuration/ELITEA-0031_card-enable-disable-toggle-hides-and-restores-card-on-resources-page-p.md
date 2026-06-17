---
id: ELITEA-0031
title: "Card Enable/Disable Toggle Hides and Restores Card on Resources Page [Parametrized: Information, Documentation, Release Notes, Video Library, Tutorials]"
priority: critical
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0031: Card Enable/Disable Toggle Hides and Restores Card on Resources Page [Parametrized: Information, Documentation, Release Notes, Video Library, Tutorials]

**Module:** Resources Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that toggling a card to Disabled removes it from the user-facing Resources page, and toggling it back to Enabled restores it. Parametrized across all 5 cards: Information, Documentation, Release Notes, Video Library, Tutorials. Covers AC3 of story #4772.

## Preconditions

Logged in as an ELITEA admin user.
All 5 cards are currently enabled.
Parameters: run separately for each card — Information, Documentation, Release Notes, Video Library, Tutorials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources. | Resources configuration page is open. |
| 2 | Locate the target card block and toggle it to Disabled. | The toggle reflects the disabled state. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Open the user-facing Resources page in any project. | The disabled card is not visible on the Resources page. |
| 5 | Return to Admin → Configuration → Resources and toggle the same card back to Enabled. | The toggle reflects the enabled state. |
| 6 | Save the configuration. | Changes are saved successfully. |
| 7 | Open the user-facing Resources page again. | The card is now visible again on the Resources page. |

## Expected Final State

The card is now visible again on the Resources page.

## Pass/Fail Criteria

Pass: Disabled card disappears from Resources page; re-enabled card reappears.
Fail: Card is still visible when disabled, or does not reappear when re-enabled.
