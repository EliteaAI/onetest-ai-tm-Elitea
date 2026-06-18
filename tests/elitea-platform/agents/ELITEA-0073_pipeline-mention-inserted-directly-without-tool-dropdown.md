---
id: ELITEA-0073
title: "Pipeline Mention Inserted Directly Without Tool Dropdown"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0073: Pipeline Mention Inserted Directly Without Tool Dropdown

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a Pipeline from autosuggest inserts the mention immediately without showing a secondary tool dropdown.

**Coverage:** No two-level selection for Pipelines; direct insertion

## Preconditions

- Agent with a pipeline added via "+ Pipeline"

## Test Data

Pipeline name; expected inserted text: /<pipeline name>

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` in Instructions. | Dropdown shows pipeline with label "Pipeline". |
| 2 | Click on the pipeline entry. | Mention /<pipeline name> inserted immediately; no second dropdown. |
| 3 | Verify bold blue highlight. | Highlight applied. |

## Expected Final State

Highlight applied.

## Pass/Fail Criteria

PASS: Pipeline mention inserted directly; no secondary dropdown; highlighted correctly
FAIL: Secondary dropdown appears; mention not inserted; incorrect format
