---
id: ELITEA-0950
title: "Project Context Content Is Truncated at 2500 Characters When Typing"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, char-limit, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0950: Project Context Content Is Truncated at 2500 Characters When Typing

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the editor enforces the 2500-character limit by truncating input at the boundary when typing or pasting.

**Coverage:**
- Editor stops accepting input at 2500 chars
- Paste is also truncated at the limit
- Save succeeds; no content beyond limit is persisted

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project Context editor. Type continuously until the character counter shows '0 characters left'. | Counter shows 0 / 2500 (or equivalent). |
| 2 | Continue typing additional characters. | Input is silently truncated — no additional characters are accepted beyond 2500. |
| 3 | Paste a large block of text that is well over 2500 characters. | Content is pasted but truncated at 2500. Counter remains at 0. |
| 4 | Click Save. | Save succeeds without error. |
| 5 | Reload the page. | Saved content is at most 2500 characters. Nothing beyond the limit was persisted. |

## Expected Final State

Saved content is at most 2500 characters. Nothing beyond the limit was persisted.

## Pass/Fail Criteria

**Pass:**
- No characters beyond 2500 accepted
- Paste truncated at limit
- Save works and persists only ≤2500 chars

**Fail:**
- Characters beyond 2500 are accepted or stored
- Save fails or throws error at the limit
