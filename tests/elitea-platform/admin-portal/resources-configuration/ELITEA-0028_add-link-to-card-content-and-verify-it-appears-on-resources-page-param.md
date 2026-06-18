---
id: ELITEA-0028
title: "Add Link to Card Content and Verify It Appears on Resources Page [Parametrized: Documentation, Release Notes, Video Library, Tutorials]"
priority: high
type: functional
module: resources-configuration
status: ready
execution_type: manual
tags: [feat:settings, story:4772, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4772]
---
# ELITEA-0028: Add Link to Card Content and Verify It Appears on Resources Page [Parametrized: Documentation, Release Notes, Video Library, Tutorials]

**Module:** Resources Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that an admin can add a new link to a card, that the link is persisted after save and page reload, and that it becomes visible to users on the Resources page. Parametrized across Documentation, Release Notes, Video Library, and Tutorials. Covers AC4 of story EliteaAI/elitea_issues#4772.

## Preconditions

Logged in as an ELITEA admin user.
The target card is enabled.
Parameters: Documentation, Release Notes, Video Library, Tutorials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Resources and open the target card section. | Card configuration is visible with its current links. |
| 2 | Click the button to add a new link. Enter a link title (e.g. Test Link) and a valid URL (e.g. https://example.com). | The new link entry appears in the card configuration. |
| 3 | Save the configuration. | Changes are saved successfully. |
| 4 | Reload the Configuration → Resources page and check the card. | The new link is present in the saved configuration. |
| 5 | Open the user-facing Resources page in any project. | The new link is visible in the target card on the Resources page. |

## Expected Final State

The new link is visible in the target card on the Resources page.

## Pass/Fail Criteria

Pass: The new link is saved and is visible to users on the Resources page.
Fail: Link is lost after save, or does not appear on Resources page.
