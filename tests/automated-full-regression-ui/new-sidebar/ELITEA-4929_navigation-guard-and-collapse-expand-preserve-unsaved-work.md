---
id: ELITEA-4929
title: "Navigation guard and collapse/expand preserve unsaved work"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4929: Navigation guard and collapse/expand preserve unsaved work

## Preconditions

- User is logged in to `{{base_url}}`
- The selected project has at least one agent and two chats

## Test Data

| # | Blocking condition | Sidebar target |
|---|--------------------|----------------|
| 1 | Unsaved edits in an agent's instructions | Explore → Pipelines |
| 2 | Unsaved edits in an agent's instructions | + New chat |
| 3 | Model is still streaming an answer in a chat | Another chat in the Chats history |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an agent and edit its instructions without saving | The page shows unsaved changes |
| 2 | Click the collapse control, then the expand control | The sidebar collapses and expands, the page doesn't change or reload, and the unsaved edits are intact |
| 3 | Click the sidebar target from Test Data row 1 | The leave-confirmation dialog appears and navigation doesn't happen yet |
| 4 | Cancel the dialog | The user stays on the agent page, the edits are kept, and the sidebar state is unchanged |
| 5 | Repeat steps 3–4 for row 2 | The same confirmation and cancel behaviour |
| 6 | Click the row 2 target again and confirm leaving | A new chat opens |
| 7 | Send a message and, while the answer is streaming, click another chat (row 3) | The leave-confirmation dialog appears, and cancel keeps the answer streaming |
| 8 | While the answer is streaming, collapse and expand the sidebar | The chat page stays open and the answer keeps streaming |

## Expected Final State

The guard fires for sidebar entry points, and toggling the sidebar never loses the user's work.

## Pass/Fail Criteria

**Pass:**
- The confirmation appears for every row, and cancel preserves the page, the work and the sidebar state
- Collapse/expand doesn't navigate, reload or lose unsaved input

**Fail:**
- Navigation happens without confirmation, or work is lost after cancel
- Collapse/expand changes the URL, reloads the page or interrupts the answer

## Notes

**Source functional tests:** ELITEA-4906, ELITEA-4909
**Regression rationale:** Data-loss risk: the new sidebar adds navigation entry points (Explore, history, New chat) that must keep going through the existing guard.
**Selected checkpoints:** Guard on Explore, New chat and history; cancel keeps work; collapse/expand keeps unsaved edits and streaming answer.
