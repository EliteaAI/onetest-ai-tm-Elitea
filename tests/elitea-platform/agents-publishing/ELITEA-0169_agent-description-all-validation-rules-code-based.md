---
id: ELITEA-0169
title: "Agent Description — All Validation Rules (Code-Based)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0169: Agent Description — All Validation Rules (Code-Based)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that all code-based validation rules for the agent Description field are applied correctly across Critical and Warning severity levels during publishing. Checks run deterministically without LLM usage.

Note: The 'empty description' Critical rule exists in the codebase but the UI now enforces non-empty descriptions at input time, making it untestable through the standard publish workflow.

## Preconditions

Agent exists with an editable Description field. Agent is not yet published (or a new version can be created).

**Test Data:**

| Row | Input Value | Check Section | Expected Severity | Expected Finding |
|-----|-------------|---------------|-------------------|------------------|
| 1 | Text fewer than 50 characters | Critical issues | Critical | Description is below minimum length (at least 50 characters required) |
| 2 | 50+ char text without action verbs (helps / generates / analyzes or similar) | Warnings | Warning | Description does not include action verbs that indicate what the agent does |
| 3 | Text containing "TODO", "TBD", or "Lorem ipsum" placeholder | Critical issues | Critical | Description contains placeholder text |
| 4 | Clear 50+ char description with action verbs, no placeholders | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set the agent Description field to the value from Row 1 of the Test Data table | Description field updated |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the section listed for Row 1 in the Test Data table (Critical issues) | Description flagged as Critical: description is too short |
| 5 | Repeat steps 1–4 for Rows 2 through 4, using the Input Value and Check Section from the Test Data table | Row 2: Warning (no action verbs); Row 3: Critical (placeholder text); Row 4: absent from all sections |

## Expected Final State

Row 2: Warning (no action verbs); Row 3: Critical (placeholder text); Row 4: absent from all sections

## Pass/Fail Criteria

Pass: All rows produce the expected severity level and message; Row 4 (valid description) produces no issue.
Fail: Any row missing its expected finding; severity mismatch; valid description incorrectly flagged.
