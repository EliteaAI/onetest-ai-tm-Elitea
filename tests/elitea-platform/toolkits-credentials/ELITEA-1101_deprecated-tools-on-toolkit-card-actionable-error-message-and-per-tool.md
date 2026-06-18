---
id: ELITEA-1101
title: "Deprecated Tools on Toolkit Card — Actionable Error Message and Per-Tool Error Icons Are Displayed"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3649]
---
# ELITEA-1101: Deprecated Tools on Toolkit Card — Actionable Error Message and Per-Tool Error Icons Are Displayed

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent configuration includes deprecated toolkit tools, the toolkit card displays both a concise actionable error message naming the invalid tools AND individual error icons on each deprecated tool entry.

**Coverage:**
- Toolkit card enters an error state when deprecated tools are referenced
- Each deprecated tool entry (`overwriteData`, `read_file_chunk`) is marked with an individual error icon
- Valid tools on the same card are NOT marked with error icons
- Top-level error message explicitly names the deprecated tools — does NOT list all valid tool names
- Error state and icons are visible immediately without hover or expansion

## Preconditions

- Logged in to ELITEA at {{base_url}}
- An Agent exists with the Artifact toolkit configured, having deprecated tools `overwriteData` and `read_file_chunk` selected

## Test Data

- Deprecated tools: `overwriteData`, `read_file_chunk`
- Valid tools (should NOT be flagged): `index_data`, `list_collections`, `search_index`
- Expected error message pattern: "The following tools are deprecated or no longer available: 'overwriteData', 'read_file_chunk'. Please remove them to continue."
- Unacceptable: "Value error, Input should be 'index_data', 'list_collections', ..."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section and open the Agent that has the Artifact toolkit with deprecated tools (`overwriteData`, `read_file_chunk`). | Agent configuration page opens. The Artifact toolkit card is visible in the toolkits section. |
| 2 | Observe the overall state of the Artifact toolkit card. | The toolkit card is visually in an error state (e.g. red border or error badge visible at the card level). |
| 3 | Read the top-level error message displayed on the toolkit card. | The message explicitly names the deprecated tools, e.g.: "The following tools are deprecated or no longer available: 'overwriteData', 'read_file_chunk'. Please remove them to continue." The message does NOT contain an enumerated list of all currently valid tool names. |
| 4 | Inspect the individual tool entries within the Artifact toolkit card. | `overwriteData` and `read_file_chunk` each have a visible error icon next to their name. Valid tools (`index_data`, `list_collections`, `search_index`) do NOT have error icons. |
| 5 | Confirm all error indicators are visible without any hover, scroll, or expansion action. | All error icons and the top-level error message are immediately visible upon opening the agent configuration page — no extra interaction required. |

## Expected Final State

All error icons and the top-level error message are immediately visible upon opening the agent configuration page — no extra interaction required.

## Pass/Fail Criteria

**Pass:**
- Error message names deprecated tools explicitly and is concise
- Each deprecated tool entry has an individual error icon
- Valid tools on the same card are not incorrectly flagged with error icons
- All error indicators are immediately visible without additional interaction

**Fail:**
- Error message shows a generic Pydantic validation error listing all valid tool names
- Deprecated tools are not individually marked with error icons
- Valid tools are also flagged with error icons (false positives)
- Error indicators only appear after hovering, scrolling, or expanding a section
