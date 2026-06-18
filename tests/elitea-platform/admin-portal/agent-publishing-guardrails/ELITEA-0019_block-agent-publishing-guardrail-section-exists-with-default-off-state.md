---
id: ELITEA-0019
title: "Block Agent Publishing Guardrail Section Exists with Default OFF State"
priority: critical
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, guardrails, story:4434, r-2.0.2, admin, p0]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0019: Block Agent Publishing Guardrail Section Exists with Default OFF State

**Module:** Agent Publishing Guardrails · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Block Agent Publishing" guardrail section exists in Admin portal, has proper styling, and the toggle is set to OFF by default.

## Preconditions

Logged into Admin portal with admin privileges
Navigate to Admin → Configuration → Guardrails

## Test Data

Admin URL: {{base_url}}
Section: Configuration → Guardrails
Expected section name: "Block Agent Publishing"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails configuration page loads |
| 2 | Scroll to locate "Block Agent Publishing" section | Section is visible on the page |
| 3 | Observe the section styling (header, layout, borders) | Section styling matches other guardrail blocks like "Blocked Toolkits" (consistent header font, spacing, border) |
| 4 | Locate the toggle control within the section | Toggle control is present and visible |
| 5 | Check the toggle state without making any changes | Toggle is in OFF state (not enabled/checked) |
| 6 | Verify no project exception dropdown is visible when toggle is OFF | Dropdown is hidden/not displayed |

## Expected Final State

Dropdown is hidden/not displayed

## Pass/Fail Criteria

PASS:
- "Block Agent Publishing" section exists in Guardrails page
- Section styling is consistent with other guardrail blocks
- Toggle control exists and is set to OFF by default
- No project exception dropdown visible when toggle is OFF

FAIL:
- Section is missing or has incorrect name
- Styling is inconsistent (different fonts, spacing, or layout)
- Toggle is ON by default
- Project exception dropdown appears when toggle is OFF
