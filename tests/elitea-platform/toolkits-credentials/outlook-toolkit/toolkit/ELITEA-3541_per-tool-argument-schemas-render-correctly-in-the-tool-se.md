---
id: ELITEA-3541
title: "Per-Tool Argument Schemas Render Correctly in the Tool Selector"
priority: medium
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3541: Per-Tool Argument Schemas Render Correctly in the Tool Selector

**Module:** Outlook Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify each of the 12 tools shows its correct name and description in the toolkit's TOOLS section, so users can identify what each tool does before selecting it.

## Preconditions

- Outlook toolkit creation/edit form open

## Test Data

- N/A (UI inspection only)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the TOOLS section of the Outlook toolkit form | All 12 tools are listed: `list_messages`, `get_message`, `send_mail`, `reply_to_message`, `mark_as_read`, `list_folders`, `move_message`, `delete_message`, `search_messages`, `check_new_messages`, `find_new_messages`, `get_thread_messages` |
| 2 | Inspect each tool's displayed name/description | Each shows a name and description accurately matching its documented behavior (no placeholder text, no mismatched descriptions) |

## Expected Final State

All 12 tools are correctly and distinctly represented in the selector UI.

## Pass/Fail Criteria

**Pass:**
- All 12 tools appear with accurate names/descriptions

**Fail:**
- Any tool is missing, mislabeled, or shows placeholder/incorrect description text
