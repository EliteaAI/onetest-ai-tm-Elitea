---
id: ELITEA-0173
title: "Tags Validation — Critical, Warning, and Info Rules (Code-Based)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0173: Tags Validation — Critical, Warning, and Info Rules (Code-Based)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that code-based validation rules for the agent Tags field are applied correctly across Critical, Warning, and Info/Suggestion severity levels during publishing. Checks run deterministically without LLM usage.

## Preconditions

Agent exists with an editable Tags field. Agent is not yet published (or a new version can be created).

**Test Data:**

| Row | Input Value | Check Section | Expected Severity | Expected Finding |
|-----|-------------|---------------|-------------------|------------------|
| 1 | (no tags added) | Critical issues | Critical | Agent has at least 1 tag (violation: no tags present) |
| 2 | All tags from generic set only (e.g. only "ai", "bot", "assistant") | Warnings | Warning | Tags are all from the generic tags set |
| 3 | More than 2 tags provided | Suggestions | Info/Suggestion | Suggest 1–2 more focused tags |
| 4 | 1–2 specific, relevant, non-generic tags | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set the agent Tags to the value from Row 1 of the Test Data table (remove all tags) | Tags field empty |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the Critical issues section | Tags flagged as Critical: agent has no tags |
| 5 | Repeat steps 1–4 for Rows 2 through 4, using the Input Value and Check Section from the Test Data table | Row 2: Warning (all generic tags); Row 3: Info/Suggestion (more than 2 tags); Row 4: absent from all sections |

## Expected Final State

Row 2: Warning (all generic tags); Row 3: Info/Suggestion (more than 2 tags); Row 4: absent from all sections

## Pass/Fail Criteria

Pass: All rows produce the expected severity; Row 4 (valid tags) produces no issue.
Fail: Any row missing its expected finding; severity mismatch (especially no-tags must be Critical not Warning); valid tags incorrectly flagged.
