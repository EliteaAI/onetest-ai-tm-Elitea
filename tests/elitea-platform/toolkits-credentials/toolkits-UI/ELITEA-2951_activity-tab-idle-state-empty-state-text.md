---
id: ELITEA-2951
title: "Activity Tab — Idle State Empty-State Text"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, activity-tab, empty-state]
requirements: []
---
# ELITEA-2951: Activity Tab — Idle State Empty-State Text

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Activity tab displays the exact idle empty-state text for an Index with no indexing activity, and that its Configuration link and "Reindex" action work correctly.

**Coverage:**
- Exact idle empty-state text
- "Configuration" link navigates to the Configuration tab
- "Reindex" displayed on Activity

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A newly created Index for which no indexing operation has been run

## Test Data

| Field | Value |
|-------|-------|
| Index | Any newly created Index with no indexing history |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index details page for a newly created Index for which no indexing operation has been run. | Page opens with "Activity" selected. |
| 2 | Inspect the displayed text. | Text reads "No indexing activity". |
| 3 | Inspect the displayed text. | Text reads "You may start reindexing with the current settings." |
| 4 | Inspect the displayed text. | Text reads "To modify them, open Configuration first." |
| 5 | Click "Configuration" within that message. | "Configuration" tab opens. |
| 6 | Click "Activity". | "Activity" tab displays again. |
| 7 | Inspect the available action. | "Reindex" is displayed. |

## Expected Final State

The idle state displays the exact three lines of text above, with a working Configuration link and Reindex available.

## Pass/Fail Criteria

**Pass:**
- All three text lines match exactly
- "Configuration" link opens the Configuration tab
- "Reindex" is displayed

**Fail:**
- Any text line is missing or worded differently
- "Configuration" link does not open Configuration
- "Reindex" is missing, or a different action is shown instead
