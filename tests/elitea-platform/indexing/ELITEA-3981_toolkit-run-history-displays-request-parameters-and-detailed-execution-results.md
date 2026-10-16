---
id: ELITEA-3981
title: "Toolkit Run History Displays Request Parameters and Detailed Execution Results"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, bug:6272, bug:6345, r-2.0.2]
requirements: [EliteaAI/elitea_issues#6272, EliteaAI/elitea_issues#6345]
---
# ELITEA-3981: Toolkit Run History Displays Request Parameters and Detailed Execution Results

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Toolkit Run History view displays complete execution details including formatted request parameters, thinking steps, tools invoked, pages indexed/skipped counts, and specific identifiers for skipped pages with reasons.

**Coverage:**
- Run History entry shows formatted request parameters JSON
- Thinking steps section displays "Thought for X secs" with expandable content
- Tools invoked section shows toolkit name and tool action (e.g., "Ado Wiki Sam: index_data")
- Execution result displays count of pages indexed
- Execution result displays count of pages skipped with reasons
- Skipped pages section lists specific page identifiers
- Layout is consistent with Index History design

## Preconditions

- Logged in to {{base_url}} with owner or editor access on a Private project
- A Toolkit with indexing capability (e.g., ADO Wiki, Confluence, SharePoint) is configured
- At least one indexing or reindexing operation has been completed on the toolkit

## Test Data

| Field | Value |
|-------|-------|
| Toolkit type | ADO Wiki (or any toolkit with index_data capability) |
| Index name | Any existing index with completed indexing history |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits & Indexes in the left navigation menu. | Toolkits list is displayed. |
| 2 | Open a toolkit that has indexing capability (e.g., ADO Wiki). | Toolkit detail page opens. |
| 3 | Run Index or Reindex. | Index / Reindex runs. |
| 4 | Click on "Run History" in the page header breadcrumb or history icon. | Run History panel opens showing a list of past operations. |
| 5 | Verify the history list shows entries with Date, Event type, and Duration columns. | Each entry displays: Date (DD-MM-YYYY, HH:MM AM/PM), Event (e.g., Indexed, Reindexed, Index data), Duration (e.g., 3.12 s). |
| 6 | Click on a completed indexing/reindexing entry in the list. | Right panel expands to show execution details with header "Calling 'index_data' with parameters". |
| 7 | Verify JSON includes relevant fields such as: max_tokens, process_attachments, ignore_empty_body, max_attachment_depth, max_attachment_size_mb, index_name. | All applicable request parameters are displayed in readable JSON format. |
| 8 | Verify the thinking steps section is displayed below the request parameters. | "Thought for X secs" label is visible with an expand/collapse arrow. |
| 9 | Click on the thinking steps section to expand it. | Thinking content is displayed, showing the LLM reasoning process. |
| 10 | Verify the tools invoked section shows the toolkit name and action. | Tools invoked displays as "[Toolkit Name]: [action]" (e.g., "Ado Wiki Sam: index_data"). |
| 11 | Verify the execution result shows count of pages/documents indexed (e.g., "246 pages indexed"). | Pages indexed count is displayed with a checkmark indicator. |
| 12 | Verify the execution result shows count of pages/documents skipped (e.g., "3 pages skipped"). | Pages skipped count is displayed with a warning indicator. |
| 13 | Verify skipped pages section lists specific identifiers and reasons (e.g., "→ Contained no indexable content (3): 12, 14, 36"). | Skipped page identifiers are listed with the reason for skipping. |

## Expected Final State

The Run History detail panel displays:
- Formatted request parameters in JSON
- Thinking steps with "Thought for X secs" label (expandable)
- Tools invoked showing toolkit name and action
- Count of pages/documents indexed
- Count of pages/documents skipped
- Specific identifiers for skipped items with reasons

## Pass/Fail Criteria

**Pass:**
- Run History entry shows formatted request parameters JSON with all relevant fields
- Thinking steps section displays "Thought for X secs" with expandable content
- Tools invoked section shows "[Toolkit Name]: [action]" format
- Execution result displays pages indexed count
- Execution result displays pages skipped count with reasons
- Skipped pages section lists specific page identifiers
- Layout is clear and consistent

**Fail:**
- Request parameters are missing or displayed as unformatted text blob
- Thinking steps are missing or not expandable
- Tools invoked section is missing or shows incorrect format
- Pages indexed/skipped counts are not shown
- Skipped pages lack specific identifiers or reasons
- Run History shows only Date and Duration without detailed execution data
