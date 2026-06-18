---
id: ELITEA-0171
title: "Sub-Agent Description — All Rules with Attribution (Code-Based, 30-Char Minimum)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0171: Sub-Agent Description — All Rules with Attribution (Code-Based, 30-Char Minimum)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that code-based validation rules for sub-agent descriptions are applied correctly across Critical and Warning severity levels, and that each finding is attributed to the specific sub-agent using the format "Sub-agent '[name]': Description [issue]".

Note: The 'empty description' Critical rule exists in the codebase but the UI now enforces non-empty descriptions at input time, making it untestable through the standard publish workflow.

## Preconditions

A parent agent with at least two sub-agents exists. Each sub-agent has an editable Description field.

**Test Data:**

| Row | Setup | Check Section | Expected Severity | Expected Finding |
|-----|-------|---------------|-------------------|------------------|
| 1 | Sub-Agent 1 description: text under 30 characters (e.g. "Fetches data.") | Warnings | Warning | "Sub-agent '[name]': Description is too short (minimum 30 characters)" |
| 2 | Sub-Agent 1 description: text containing "TODO", "TBD", or "Lorem ipsum" | Critical issues | Critical | "Sub-agent '[name]': Description contains placeholder text" |
| 3 | Sub-Agent 1 description: clear text of at least 30 characters, no placeholder | All sections | None | No issue raised |
| 4 | Sub-Agent 1 description: text under 30 characters (e.g. "Fetches data."); Sub-Agent 2 description: text under 30 characters (e.g. "Gets info.") | Warnings | Warning | Two separate findings — one per sub-agent: "Sub-agent '[name]': Description is too short (minimum 30 characters)" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Sub-Agent 1 (and Sub-Agent 2 if needed) per the Setup column of Row 1 | Sub-agent description(s) updated as specified |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the section listed for Row 1 (Warnings) and confirm the finding matches the Expected Finding column | Warning present, attributed to the specific sub-agent by name in correct format |
| 5 | Repeat steps 1–4 for Rows 2 through 4, applying the Setup from each row | Row 2: Critical (placeholder text) with attribution; Row 3: absent from all sections; Row 4: two separate Warning findings (too short, <30 chars) attributed individually to each sub-agent — not merged into one entry |

## Expected Final State

Row 2: Critical (placeholder text) with attribution; Row 3: absent from all sections; Row 4: two separate Warning findings (too short, <30 chars) attributed individually to each sub-agent — not merged into one entry

## Pass/Fail Criteria

Pass: All rows produce the expected severity and finding; each finding is attributed to the specific sub-agent by name; Row 4 produces two separate Warning entries (not merged); Row 3 produces no issue.
Fail: Any row missing its expected finding; severity mismatch; attribution absent or in wrong format; duplicate too-short findings merged into one; valid description incorrectly flagged.
