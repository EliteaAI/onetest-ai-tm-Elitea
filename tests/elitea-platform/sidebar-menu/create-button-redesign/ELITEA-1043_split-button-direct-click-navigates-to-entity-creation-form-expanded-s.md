---
id: ELITEA-1043
title: "Split Button Direct-Click Navigates to Entity Creation Form (Expanded Sidebar)"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1043: Split Button Direct-Click Navigates to Entity Creation Form (Expanded Sidebar)

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that left-clicking the label part of the split button opens the correct entity creation form for each section.

**Coverage:**
- Click action for all 8 main sections
- Correct destination form/page per section

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar is in expanded state
- Any project selected

## Test Data

All 8 main sections: Chat, Agents, Pipelines, Credentials, Toolkits, Applications, MCP, Artifacts

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents; click the `+ Agent` label (left part of split button) | New Agent creation form opens |
| 2 | Navigate to Pipelines; click `+ Pipeline` label | New Pipeline creation form opens |
| 3 | Navigate to Chat; click `+ Conversation` label | New conversation / chat input is initiated |
| 4 | Navigate to Credentials; click `+ Credential` label | New Credential creation form opens |
| 5 | Navigate to Toolkits; click `+ Toolkit` label | New Toolkit creation form opens |
| 6 | Navigate to Applications; click `+ Application` label | New Application configuration/creation flow opens |
| 7 | Navigate to MCP; click `+ MCP` label | New MCP creation form opens |
| 8 | Navigate to Artifacts; click `+ Artifact Bucket` label | New Artifact Bucket creation form opens |

## Expected Final State

New Artifact Bucket creation form opens

## Pass/Fail Criteria

**Pass:**
- Each direct click opens the correct creation form for that section's entity type

**Fail:**
- Click opens wrong form or navigates to wrong page
- Nothing happens on click
- Dropdown opens instead of navigating directly
