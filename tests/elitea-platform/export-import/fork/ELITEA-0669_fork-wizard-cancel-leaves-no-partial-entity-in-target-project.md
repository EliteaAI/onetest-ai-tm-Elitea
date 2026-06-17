---
id: ELITEA-0669
title: "Fork Wizard Cancel Leaves No Partial Entity in Target Project"
priority: medium
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0669: Fork Wizard Cancel Leaves No Partial Entity in Target Project

**Module:** Fork · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that cancelling the fork wizard at any step performs no partial operation and leaves no orphaned entity in any project.

**Coverage:**
- Cancel at target project selection step
- Cancel after target project selected but before confirming
- No side effects on Target Project
- Clean return to source entity

## Preconditions

- Logged in as Editor in Source Project and Target Project

## Test Data

- Any agent in Source Project
- Target Project: any valid project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Fork wizard for any agent | Wizard opens |
| 2 | Select a Target Project | Target Project selected |
| 3 | Click Cancel (or close the modal with X) before clicking Fork | Wizard closes |
| 4 | Navigate to Target Project → Agents | Agents list opens |
| 5 | Confirm the cancelled agent is not present in Target Project | Agent absent |
| 6 | Verify the user is returned to or can easily navigate back to the source agent page | Source agent accessible |

## Expected Final State

Source agent accessible

## Pass/Fail Criteria

**Pass:**
- No entity created in Target Project after cancellation
- No errors thrown during cancel
- User can resume normal navigation

**Fail:**
- A partial or empty agent record appears in Target Project after cancel
- UI throws an error on cancel
- User is unexpectedly redirected away from the source
