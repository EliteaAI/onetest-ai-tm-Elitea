---
id: ELITEA-4232
title: "Verify Project/Shared indicator renders correctly with long names, narrow window, long list and keyboard navigation"
priority: medium
type: functional
module: llm-selector
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is Editor or Admin in Team Project A
- Team Project A has 15 or more LLM models available in total (project-level plus Shared)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Long model display name | `QA-7057-Very-Long-Model-Display-Name-For-Truncation-Check-1234567890` |
| Narrow window width | 1024 px |
| Minimum list size | 15 models |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Project A, go to Settings → AI Configuration and create a project LLM configuration with display name `QA-7057-Very-Long-Model-Display-Name-For-Truncation-Check-1234567890` | The configuration is saved and appears in the list |
| 2 | Go to Chats, open a conversation and open the LLM model dropdown | The long name entry is shown truncated (e.g. with ellipsis); the Project indicator remains fully visible and is not overlapped |
| 3 | Resize the browser window to 1024 px wide and open the dropdown again | The long name is still truncated; the indicator remains visible; no horizontal overflow of the dropdown |
| 4 | Scroll through the full list of 15+ models | Indicators on entries that scroll into view render correctly and match each model's source |
| 5 | Close and reopen the dropdown; use the Down/Up arrow keys to move through entries | The highlight moves entry by entry; indicators stay visible on the highlighted entry |
| 6 | Press Enter on a highlighted entry | The entry is selected; the dropdown closes and the button label shows the chosen model |

## Expected Final State

The Project/Shared indicator stays visible and correct for long names, at 1024 px width, while scrolling a long list and during keyboard navigation; keyboard selection works.

## Pass/Fail Criteria

**Pass:**
- Long names truncate without hiding or overlapping the indicator
- Indicators render correctly at 1024 px and on scrolled-in entries
- Arrow-key highlighting and Enter selection work

**Fail:**
- The indicator is clipped, hidden, overlapped or misaligned in any condition
- Entries that scroll into view have no indicator or the wrong one
- Keyboard navigation or Enter selection does not work
