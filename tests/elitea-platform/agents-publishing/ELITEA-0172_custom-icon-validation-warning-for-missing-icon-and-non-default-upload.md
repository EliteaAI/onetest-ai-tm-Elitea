---
id: ELITEA-0172
title: "Custom Icon Validation — Warning for Missing Icon and Non-Default Upload (Code-Based)"
priority: medium
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0172: Custom Icon Validation — Warning for Missing Icon and Non-Default Upload (Code-Based)

**Module:** Agents Publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that code-based icon validation correctly flags a missing icon as a Warning and passes silently when the agent uses an icon  (selected from the default icon list OR custom one).

## Preconditions

Agent with a configurable icon field exists. Agent is not yet published (or a new version can be created).

**Test Data:**

| Scenario | Icon State | Check Section | Expected Severity | Expected Finding |
|----------|------------|---------------|-------------------|------------------|
| 1 | No icon set (icon_meta empty) | Warnings | Warning | "Add a custom icon to improve marketplace visibility" |
| 2 | Icon selected from the platform default icon list | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure the agent has no icon set (icon_meta empty) | Icon field empty or shows placeholder |
| 2 | Click Publish | Publish modal opens |
| 3 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the Warnings section | Icon warning listed: "Add a custom icon to improve marketplace visibility" |
| 5 | Set the agent icon (custom or from default icon list) | Icon applied to the agent |
| 6 | Click Publish | Publish modal opens |
| 7 | Enter a valid version name, accept the agreement, click Publish | Validation runs; results panel shown |
| 8 | Check all sections for any icon-related issue | Icon absent from all sections (no warning, no critical, no suggestion) |

## Expected Final State

Icon absent from all sections (no warning, no critical, no suggestion)

## Pass/Fail Criteria

Pass: Scenario 1 → Warning with "Add a custom icon" message; Scenario 2 → absent from all sections.
Fail: Scenario 1 not flagged; Scenario 2 incorrectly flagged; any scenario shows wrong message or wrong section.
