---
id: ELITEA-0812
title: "Pipeline — Save New Version Redirects to Newly Created Version"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [nfr:usability, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3903]
---
# ELITEA-0812: Pipeline — Save New Version Redirects to Newly Created Version

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that saving a pipeline as a new version redirects the user to the newly created version page instead of showing a "No Page Found" error.

## Preconditions

User is logged in to ELITEA
At least one Pipeline exists in the project
User has edit permissions for the Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Pipeline configuration page | Pipeline config page loads; version selector shows the current version name |
| 2 | Make a minor change (e.g., edit a node task field) | Save button becomes active |
| 3 | Click Save → select 'Save as new version' → enter name 'test-v2' → confirm | Dialog closes; no error message appears |
| 4 | Observe the page after save completes | User is redirected to the newly created version page; version selector shows 'test-v2'; page is fully functional with no error displayed |

## Expected Final State

User is redirected to the newly created version page; version selector shows 'test-v2'; page is fully functional with no error displayed

## Pass/Fail Criteria

PASS: User is redirected to new version page; version selector shows 'test-v2'; no error page is shown
FAIL: 'No Page Found' or any error page is displayed after saving the new version
