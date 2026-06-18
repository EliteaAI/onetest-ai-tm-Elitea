---
id: ELITEA-1028
title: "Collapsed Sidebar Dropdown: Correct Order of All Entity Types"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1028: Collapsed Sidebar Dropdown: Correct Order of All Entity Types

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that all entity types appear in the correct order in the collapsed sidebar dropdown.

**Coverage:**
- Complete list presence and order in collapsed dropdown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in collapsed state

## Test Data

Expected order: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse sidebar; click `+` | Dropdown opens |
| 2 | Inspect the full list of items top to bottom | Items appear in this order: Conversation → Agent → Pipeline → Credential → Toolkit → MCP → Artifact Bucket → Integration → Secret → Token → User Invite |
| 3 | Navigate to a different section; reopen the dropdown | Order remains consistent |

## Expected Final State

Order remains consistent

## Pass/Fail Criteria

**Pass:**
- All 11 entity types are present in the correct order

**Fail:**
- Any entity type is missing
- Order differs from the specified sequence
