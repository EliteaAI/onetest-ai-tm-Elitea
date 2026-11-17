---
id: ELITEA-4695
title: "New Pipeline — Auto-filled General Info and Name Validation"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7154]
---
# ELITEA-4695: New Pipeline — Auto-filled General Info and Name Validation

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking **+ Pipeline** opens the editor directly on the canvas with an auto-filled name, that only Name is required, and that the Name field validates empty, whitespace-only, too-long and special-character input correctly.

**Coverage:**
- Editor opens directly on the canvas (no intermediate form)
- Default name is count-based (`Pipeline <total pipelines + 1>`)
- Description and Tags are optional
- Name validation: empty, whitespace-only, 32-character limit, trimming, special characters / emoji
- Duplicate pipeline names are allowed
- Left-panel sections present and unchanged
- Unsaved-changes warning when leaving

## Preconditions

- Logged in to {{base_url}}
- A project with a known number of existing pipelines (note the count N)

## Test Data

- Name with spaces around: `   Pipeline X   `
- Whitespace-only name: `   `
- 32-character name: `abcdefghijklmnopqrstuvwxyz123456`
- Special characters: `Pipeline_Test-#1 (QA)`
- Emoji: `🚀 Pipeline Test`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Go to Pipelines and click **+ Pipeline**. | Editor opens directly with breadcrumb `Pipelines / New Pipeline` and the canvas visible. No name/description form is shown first. |
| 2 | Observe the Name field. | Name is pre-filled as `Pipeline <N+1>` (count-based: total number of pipelines in the project + 1, regardless of existing names). |
| 3 | Observe Description and Tags. | Both are empty and not marked as required (no asterisk). |
| 4 | Observe the header buttons. | **Save** is enabled. **Cancel** is disabled (it becomes enabled after switching to the Yaml tab — intended). |
| 5 | Observe the left panel sections. | TOOLS shows *"Tools you select in nodes will appear here."*; MODULES shows the **Attachments** toggle (off); WELCOME MESSAGE shows the placeholder *"Input your welcome message"*; CHAT STARTERS shows **+ Starter** and *"0/6 starters added."*; ADVANCED shows **Step limit 25**; EDITOR NOTES is present. |
| 6 | Hover the info icon next to **Step limit**. | Tooltip: *"The maximum number of steps to take before ending the execution loop (tools call limit)."* |
| 7 | Hover the info icon next to **Editor notes**. | Tooltip: *"Free-text notes for documentation only. Not sent to the LLM, chat, or execution; not used in monitoring."* |
| 8 | Clear the Name field completely. | **Save** becomes disabled. |
| 9 | Enter whitespace only (`   `). | Save is blocked; inline error **"Name is required."** is shown. |
| 10 | Enter `   Pipeline X   ` and Save. | Pipeline saves; name is stored trimmed as `Pipeline X`. |
| 11 | Edit Name to the 32-character value, then try to type a 33rd character. | 32 characters are accepted; the 33rd character is blocked by the input. |
| 12 | Edit Name to `Pipeline_Test-#1 (QA)` and Save. | Saves successfully and displays correctly in the pipelines list. |
| 13 | Edit Name to `🚀 Pipeline Test` and Save. | Saves successfully and displays correctly in the pipelines list. |
| 14 | Create another new pipeline and set its name to an existing pipeline's exact name. Save. | Save succeeds — duplicate pipeline names are allowed. |
| 15 | Create a new pipeline, make no changes, click **Pipelines** in the breadcrumb. | Navigates back silently; no warning; nothing is saved. |
| 16 | Create a new pipeline, make any change (e.g. edit the name), click **Pipelines** in the breadcrumb. | Warning modal: *"Warning — There are unsaved changes. Are you sure you want to leave?"* with **Cancel** / **Leave**. Known: elitea_issues#7295 (first save after a rename shows this warning unexpectedly). |

## Expected Final State

New pipelines open canvas-first with a count-based default name; only Name is required and it is validated (empty/whitespace blocked, 32-char limit, trimming); special characters, emoji and duplicate names are accepted.

## Pass/Fail Criteria

**Pass:**
- Editor opens directly on the canvas with an auto-filled count-based name
- Description and Tags are optional
- Empty/whitespace names block Save with "Name is required."
- 32-character limit enforced; surrounding spaces trimmed
- Special characters, emoji and duplicate names save correctly
- Unsaved-changes warning appears only when changes exist

**Fail:**
- An intermediate create form appears
- Save is possible with an empty or whitespace-only name
- Names over 32 characters are accepted
- Leaving with changes shows no warning, or leaving without changes shows a warning
