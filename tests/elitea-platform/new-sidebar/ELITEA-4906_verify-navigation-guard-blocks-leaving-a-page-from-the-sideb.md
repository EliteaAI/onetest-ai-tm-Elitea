---
id: ELITEA-4906
title: "Verify navigation guard blocks leaving a page from the sidebar"
priority: high
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562, EliteaAI/elitea_issues#7560]
---
# ELITEA-4906: Verify navigation guard blocks leaving a page from the sidebar


## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| # | Blocking condition | Sidebar target |
|---|--------------------|----------------|
| 1 | Unsaved edits in an agent's configuration | Explore → Pipelines |
| 2 | Model is still streaming an answer in a chat | Another chat in the Chats history |
| 3 | Unsaved edits in an agent's configuration | + New chat |
| 4 | Model is still streaming an answer in a chat | Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create the blocking condition from the Test Data row | The page is in a "dirty" or answering state |
| 2 | Click the sidebar target from the same row | The existing leave-confirmation dialog appears and navigation doesn't happen yet |
| 3 | Cancel the dialog | The user stays on the page, the edits or answer are kept, and the sidebar state is unchanged |
| 4 | Click the target again and confirm leaving | Navigation to the target happens |
| 5 | Repeat for every Test Data row | The same behaviour for every row |

## Expected Final State

The guard fires for every sidebar entry point, and cancel keeps the user's work.

## Pass/Fail Criteria

**Pass:**
- The confirmation appears for every row, and cancel preserves the page and sidebar state

**Fail:**
- Navigation happens without confirmation, or the work is lost after cancel
