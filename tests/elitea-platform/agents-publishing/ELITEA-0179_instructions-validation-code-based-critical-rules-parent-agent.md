---
id: ELITEA-0179
title: "Instructions Validation — Code-Based Critical Rules (Parent Agent)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0179: Instructions Validation — Code-Based Critical Rules (Parent Agent)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify the code-based validation flags the correct severity for each Instructions rule for the parent agent. Only deterministic checks are applied — no AI/LLM-based analysis.

**Coverage:**
- Empty instructions → Critical
- Instructions < 100 characters → Critical
- Placeholder text (TODO / TBD / Lorem ipsum) → Critical
- Valid instructions (≥100 chars, no placeholder) → No issue

## Preconditions

Agent with editable Instructions field. Agent is not yet published.

## Test Data

| Row | Instructions value | Expected section |
|-----|-------------------|------------------|
| A | (empty) | Critical issues |
| B | "Help users." (under 100 chars) | Critical issues |
| C | "TODO: add instructions here" (placeholder text) | Critical issues |
| D | 100+ chars, clear directives, no placeholder text | Absent from all sections |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Instructions to the value from the current row (repeat for rows A–D) | Field updated |
| 2 | Click Publish → enter version name → accept agreement → click Publish | Validation runs; results panel shown |
| 3 | Check the section listed in the Expected column for the current row | Instructions issue appears in the expected section (or is absent for Row D) |

## Expected Final State

Instructions issue appears in the expected section (or is absent for Row D)

## Pass/Fail Criteria

Pass: Rows A, B, C each produce a Critical issue; Row D produces no issue.
Fail: Any Critical scenario is absent, appears as Warning, or is in wrong section; valid instructions incorrectly flagged.
