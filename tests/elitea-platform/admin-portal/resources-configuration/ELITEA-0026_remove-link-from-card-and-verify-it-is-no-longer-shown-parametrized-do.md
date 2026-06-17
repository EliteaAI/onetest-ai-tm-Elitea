---
id: ELITEA-0026
title: "Remove Link from Card and Verify It Is No Longer Shown [Parametrized: Documentation, Release Notes, Video Library, Tutorials]"
priority: high
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0026: Remove Link from Card and Verify It Is No Longer Shown [Parametrized: Documentation, Release Notes, Video Library, Tutorials]

**Module:** Resources Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that an admin can remove a link from a card, that the link is no longer present in the saved configuration after page reload, and that it no longer appears on the user-facing Resources page. Parametrized across Documentation, Release Notes, Video Library, and Tutorials. Covers AC4 of story #4772.

## Preconditions

Logged in as an ELITEA admin user.
The target card has at least one existing link.
Parameters: Documentation, Release Notes, Video Library, Tutorials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources and open the target card section. | Card configuration is visible with at least one existing link. |
| 2 | Click the Remove (delete) button next to one of the existing links. | The link is removed from the list in the configuration form. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Reload the Configuration → Resources page and check the same card. | The removed link is no longer present in the configuration. |
| 5 | Open the user-facing Resources page in any project and locate the target card. | The removed link is not visible on the Resources page. |

## Expected Final State

The removed link is not visible on the Resources page.

## Pass/Fail Criteria

Pass: Removed link is no longer in saved config and is absent from the user-facing page.
Fail: Removed link still appears after save or on the Resources page.
