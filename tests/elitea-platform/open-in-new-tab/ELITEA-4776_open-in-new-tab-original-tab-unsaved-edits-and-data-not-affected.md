---
id: ELITEA-4776
title: "Open in new tab: Original tab, unsaved edits and data are not affected"
priority: high
type: functional
module: open-in-new-tab
status: ready
execution_type: manual
tags: [open-in-new-tab, unsaved-changes, no-side-effects, release:2.0.9, issue:7478]
requirements: [EliteaAI/elitea_issues#7478]
---
# ELITEA-4776: Open in new tab: Original tab, unsaved edits and data are not affected

**Module:** open-in-new-tab · **Priority:** High · **Type:** Functional

**Objective:** Verify that opening links in a new tab does not lose unsaved edits, trigger actions, or change data, and that state-changing controls remain buttons.

**Coverage:**
- Unsaved edits in the original tab
- No data side effects
- Save / Delete / Run / toggles are not links

## Preconditions
- User is logged in; an Agent exists.
- The agent configuration page is open with an unsaved edit (e.g., changed description).

## Test Data
- Agent `QA-Agent-NewTab`; edited description text `Unsaved edit check`

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | From the edited agent page, Ctrl/Cmd+Click a sidebar item | Destination opens in a new tab |
| 2 | Right-click a breadcrumb or linked item on the page → "Open link in new tab" | Destination opens in a new tab |
| 3 | Return to the original tab | Unsaved edit is still present; no unsaved-changes prompt, no reload |
| 4 | Check Run History, the entity list and entity counts | No entity was created, run, or modified |
| 5 | Right-click **Save**, **Delete**, **Run** and a toggle | No "Open link in new tab" option; they remain buttons |

## Expected Final State
Original tab keeps its unsaved edits; data is unchanged; action controls are not links.

## Pass/Fail Criteria
- **Pass:** Edits are preserved, no side effects occur, and action controls offer no link option.
- **Fail:** Edits are lost, a prompt/reload appears, data changes, or an action control behaves as a link.
