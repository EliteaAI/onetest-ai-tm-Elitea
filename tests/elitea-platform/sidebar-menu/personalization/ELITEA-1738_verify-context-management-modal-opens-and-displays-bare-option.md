---
id: ELITEA-1738
title: "Verify Context Management modal opens and displays Bare option"
priority: critical
type: functional
module: context-management
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1738: Verify Context Management modal opens and displays Bare option

**Module:** Context Management · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Context Management modal opens correctly and includes the Bare personality option in USER INSTRUCTIONS section

## Preconditions

- User is logged in to `{{base_url}}`
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Modal Name | Context Management |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chat page | Chat interface loads |
| 2 | Create new chat or open existing chat | Chat is active |
| 3 | Locate and click "Edit context settings" button | Button is found and clicked |
| 4 | Verify "Context Management" modal opens | Modal appears with title "Context Management" and close button (×) |
| 5 | Verify modal displays three metric cards at top: Tokens (233 / 64 000), Messages (2), Summaries (0) | All three metrics are visible with example values |
| 6 | Verify "CONTEXT STRATEGY & TOKEN MANAGEMENT" section is visible | Section is present and expanded |
| 7 | Verify "SUMMARIZATION" section is visible | Section is present |
| 8 | Scroll to bottom and verify "USER INSTRUCTIONS" section is visible | USER INSTRUCTIONS section exists at bottom of modal |
| 9 | Verify modal is scrollable if content exceeds viewport height | Modal scrolls properly |

## Expected Final State

Context Management modal is open showing all sections including USER INSTRUCTIONS with persona dropdown.

## Pass/Fail Criteria

**Pass:**
- Modal opens successfully
- All sections (CONTEXT STRATEGY, SUMMARIZATION, USER INSTRUCTIONS) are visible
- Modal layout is correct with no overlapping elements
- Close button (×) is present

**Fail:**
- Modal fails to open
- Sections are missing or incorrectly labeled
- Layout is broken or elements overlap
