---
id: ELITEA-0168
title: "Sub-Agent Name — All Rules with Attribution and Uniqueness Enforcement (Code-Based)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0168: Sub-Agent Name — All Rules with Attribution and Uniqueness Enforcement (Code-Based)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that code-based validation rules for sub-agent names are applied correctly across Critical and Warning severity levels, that each finding is attributed to the specific sub-agent, and that duplicate sub-agent names are flagged as Critical.

Note: The 'empty name' Critical rule exists in the codebase but the UI now enforces non-empty names at input time, making it untestable through the standard publish workflow.

## Preconditions

A parent agent with at least two sub-agents exists. Each sub-agent has an editable Name field.

**Test Data:**

| Row | Setup | Check Section | Expected Severity | Expected Finding |
|-----|-------|---------------|-------------------|------------------|
| 1 | Sub-Agent 1 name: "AB" (2 characters) | Warnings | Warning | "Sub-agent '[name]': Name is below 3 characters (valid range: 3–32)" |
| 2 | Sub-Agent 1 name: string of 33+ characters | Warnings | Warning | "Sub-agent '[name]': Name exceeds 32 characters (valid range: 3–32)" |
| 3 | Sub-Agent 1 name: "test" or "agent" (generic blocklist value) | Warnings | Warning | "Sub-agent '[name]': Name is from the generic names blocklist" |
| 4 | Sub-Agent 1 name: "TODO: Sub-agent" or "TBD" | Critical issues | Critical | "Sub-agent '[name]': Name contains placeholder text" |
| 5 | Sub-Agent 1 name: "DataFetcher"; Sub-Agent 2 name: "DataFetcher" (duplicate) | Critical issues | Critical | Two separate findings: "Sub-agent 'DataFetcher': Name must be unique across all sub-agents" — one per sub-agent |
| 6 | Sub-Agent 1 name: unique, descriptive, 3–32 char, non-generic, non-placeholder | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Sub-Agent 1 (and Sub-Agent 2 if needed) per the Setup column of Row 1 | Sub-agent name(s) updated as specified |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the section listed for Row 1 (Warnings) and confirm the finding matches the Expected Finding column | Warning present, attributed to the specific sub-agent by name in correct format |
| 5 | Repeat steps 1–4 for Rows 2 through 6, applying the Setup from each row | Row 2: Warning (too long); Row 3: Warning (generic blocklist); Row 4: Critical (placeholder text); Row 5: two separate Critical findings attributed to each 'DataFetcher' sub-agent; Row 6: absent from all sections |

## Expected Final State

Row 2: Warning (too long); Row 3: Warning (generic blocklist); Row 4: Critical (placeholder text); Row 5: two separate Critical findings attributed to each 'DataFetcher' sub-agent; Row 6: absent from all sections

## Pass/Fail Criteria

Pass: All rows produce the expected severity and finding; each finding is attributed to the specific sub-agent by name; Row 5 produces two separate Critical entries (not merged); Row 6 produces no issue.
Fail: Any row missing its expected finding; severity mismatch; attribution absent; duplicate-name findings merged into one; valid name incorrectly flagged.
