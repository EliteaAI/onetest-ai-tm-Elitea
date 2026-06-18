---
id: ELITEA-0668
title: "Fork Complete State Shows Correct Navigation Link to New Entity"
priority: medium
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0668: Fork Complete State Shows Correct Navigation Link to New Entity

**Module:** Fork · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after a successful fork the wizard displays a "Fork Complete" state with a working navigation link to the newly created entity in the target project.

**Coverage:**
- Wizard success state title
- Navigation link to new entity
- Link correctness (correct project, correct entity)
- Wizard close behaviour

## Preconditions

- Logged in as Editor; fork operation can be completed successfully

## Test Data

- Any agent in Source Project
- Any valid Target Project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Fork any agent to a Target Project | Fork completes |
| 2 | Observe wizard header/title | Title changes to "Fork Complete" |
| 3 | Verify a clickable link("Got it" button) to the new entity is displayed in the modal | "Got it" button should be displayed and active. |
| 4 | Click on the button | Browser navigates to the forked agent in Target Project (correct project and entity ID in URL) |
| 5 | Now click go back | Browser navigates to the main agent in the source project without any issue |

## Expected Final State

Browser navigates to the main agent in the source project without any issue

## Pass/Fail Criteria

**Pass:**
- Modal title is "Fork Complete" after success
- Link navigates to the correct forked entity in the correct target project
- Wizard closes cleanly

**Fail:**
- Modal still shows "Fork parameters" or stays in loading state
- No navigation link is shown
- Link navigates to wrong entity or project
