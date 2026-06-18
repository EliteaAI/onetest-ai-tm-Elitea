---
id: ELITEA-1166
title: "TC-013: Confluence Toolkit Functional Regression — Tool Call Succeeds After UI Reorganization"
priority: high
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1166: TC-013: Confluence Toolkit Functional Regression — Tool Call Succeeds After UI Reorganization

**Module:** Confluence Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Regression test — verify that after the UI reorganization, a Confluence toolkit created through the new form can successfully execute a tool call (e.g., search pages, get page) and return a valid Confluence API response. The UI change should not affect backend functionality.

Coverage:
- New-form toolkit authenticates and connects to Confluence
- A tool call (e.g., Search Pages) returns a valid response, not an error

## Preconditions

- Logged in as User A with access to a real or sandbox Confluence instance
- Valid Confluence credentials available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Confluence toolkit creation form and fill all required fields using the new reorganized layout | All 9 visible fields present and accepting input |
| 2 | Save the toolkit | Saved successfully; no errors displayed |
| 3 | Open the toolkit's Test Settings / tool invocation panel | Panel opens and shows available Confluence tools |
| 4 | Select a read tool (e.g., 'Search Pages' or 'Get Page') and invoke it with minimal valid parameters | Tool call executes without error |
| 5 | Observe the response | Valid Confluence API response returned (page data or search results) — not an authentication error or 500 |

## Expected Final State

Valid Confluence API response returned (page data or search results) — not an authentication error or 500

## Pass/Fail Criteria

PASS:
- Tool call returns a valid Confluence API response (page data, search results, etc.) — not an error
- No authentication errors or 500s

FAIL:
- Tool call returns authentication error or 500
- Toolkit cannot be saved
- Connection test fails when it should succeed
