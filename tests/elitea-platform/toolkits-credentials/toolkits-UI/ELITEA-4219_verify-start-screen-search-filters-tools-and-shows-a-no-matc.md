---
id: ELITEA-4219
title: "Verify start screen search filters tools and shows a no-match message"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7045]
---
# ELITEA-4219: Verify start screen search filters tools and shows a no-match message

## Preconditions

- User is logged in to `{{base_url}}`
- Private project is selected
- Toolkit `Jira_Management` exists with tool groups

## Test Data

| Input | Expected list |
|-------|---------------|
| `issue` | Only tools whose name contains "issue" |
| `ISSUE` | Same result as `issue` |
| `  issue  ` (spaces at start and end) | Same result as `issue` |
| `zzz_nomatch` | Message `No tools match "zzz_nomatch".` |
| `<script>alert(1)</script>` | Shown as plain text in the no-match message; no script runs |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `Jira_Management` and click **Test**. | The start screen opens. |
| 2 | Without clicking, start typing `issue`. | The text appears in the "Search tools..." field (the field has focus by default). |
| 3 | Look at the list for `issue`. | Only tools whose name contains "issue" are shown. |
| 4 | Look at the group headers. | Headers of groups with no matching tools are hidden. |
| 5 | Replace the text with `ISSUE`. | The same tools as in step 3 are shown. |
| 6 | Replace the text with `  issue  `. | The same tools as in step 3 are shown. |
| 7 | Replace the text with `zzz_nomatch`. | No tools are shown; the message `No tools match "zzz_nomatch".` is shown. |
| 8 | Replace the text with `<script>alert(1)</script>`. | The no-match message shows the input as plain text; no alert or script runs. |
| 9 | Delete all text in the search field. | The full grouped tool list is shown again. |

## Expected Final State

The search field filters the start-screen tools case-insensitively, ignores spaces at the start and end, and shows a safe no-match message.

## Pass/Fail Criteria

**Pass:**
- The search field has focus when the start screen opens
- Filtering is case-insensitive and ignores spaces at the start and end
- Empty groups are hidden; the no-match message is shown and escapes HTML

**Fail:**
- The user must click the field before typing
- Filtering is case-sensitive or misses matching tools
- Empty group headers stay visible, no message is shown, or the script runs
