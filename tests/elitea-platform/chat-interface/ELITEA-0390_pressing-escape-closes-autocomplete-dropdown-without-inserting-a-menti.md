---
id: ELITEA-0390
title: "Pressing Escape closes autocomplete dropdown without inserting a mention"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4896]
---
# ELITEA-0390: Pressing Escape closes autocomplete dropdown without inserting a mention

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that pressing Escape while the autocomplete dropdown is open dismisses it without inserting any mention and leaves the input field content unchanged.

**Coverage:**
- Escape key dismisses the autocomplete dropdown
- Input field content (including the typed `@` and filter text) is unchanged after Escape
- No mention is inserted on Escape
- User can continue typing plain text normally after dismissal

## Preconditions

- Logged into ELITEA at {{base_url}}
- A conversation with at least 1 other participant is open

## Test Data

| Data | Value |
|---|---|
| Pre-existing text before `@` | `Hello ` |
| Characters typed including trigger | `@Bo` |
| Full input before Escape | `Hello @Bo` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the conversation; type `Hello ` then `@Bo` in the input | Autocomplete dropdown appears filtered to "Bob" |
| 2 | Press Escape | Dropdown closes; no mention is inserted |
| 3 | Verify the input field content | Input still shows `Hello @Bo` unchanged as plain text |
| 4 | Continue typing ` world` | Input reads `Hello @Bo world`; no mention chip or special formatting applied |

## Expected Final State

Input reads `Hello @Bo world`; no mention chip or special formatting applied

## Pass/Fail Criteria

**Pass:**
- Dropdown disappears immediately on Escape
- `Hello @Bo` is preserved verbatim; nothing is inserted or removed
- User can type normally after dismissal

**Fail:**
- Escape submits the message or clears the input field
- A mention is inserted despite pressing Escape
- Dropdown does not respond to Escape
