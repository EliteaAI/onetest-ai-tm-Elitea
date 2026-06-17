---
id: ELITEA-0170
title: "Agent Name — All Validation Rules (Code-Based)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0170: Agent Name — All Validation Rules (Code-Based)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that all code-based validation rules for the agent Name field are applied correctly across Critical and Warning severity levels during publishing. Checks run deterministically without LLM usage.

Note: The 'empty name' Critical rule exists in the codebase but the UI now enforces non-empty names at input time, making it untestable through the standard publish workflow.

## Preconditions

Agent exists with an editable Name field. Agent is not yet published (or a new version can be created).

**Test Data:**

| Row | Input Value | Check Section | Expected Severity | Expected Finding |
|-----|-------------|---------------|-------------------|------------------|
| 1 | "AB" (2 characters) | Warnings | Warning | Name is below 3 characters (valid range: 3–32) |
| 2 | String of 33+ characters | Warnings | Warning | Name exceeds 32 characters (valid range: 3–32) |
| 3 | "test" or "agent" (generic blocklist value) | Warnings | Warning | Name is from the generic names blocklist |
| 4 | "TODO: My Agent" or "TBD" (placeholder text) | Critical issues | Critical | Name contains placeholder text (TODO/TBD) |
| 5 | Descriptive, unique, 3–32 char, non-generic, non-placeholder name | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set the agent Name field to the value from Row 1 of the Test Data table | Name field updated |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the section listed for Row 1 in the Test Data table (Warnings) | Warning present: name is too short |
| 5 | Repeat steps 1–4 for Rows 2 through 5, entering the name from the Test Data table per row | Row 2: Warning (too long); Row 3: Warning (generic blocklist); Row 4: Critical (placeholder text); Row 5: absent from all sections |

## Expected Final State

Row 2: Warning (too long); Row 3: Warning (generic blocklist); Row 4: Critical (placeholder text); Row 5: absent from all sections

## Pass/Fail Criteria

Pass: All rows produce the expected severity level; Row 5 (valid name) produces no issue.
Fail: Any row missing its expected finding; severity mismatch on any row; valid name incorrectly flagged.
