---
id: ELITEA-1042
title: "Create Button Label Accuracy in Expanded Sidebar — Main Sections"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1042: Create Button Label Accuracy in Expanded Sidebar — Main Sections

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Create button displays the correct entity-specific label for each main navigation section when the sidebar is expanded.

**Coverage:**
- Label `+ Conversation` on Chat
- Label `+ Agent` on Agents
- Label `+ Pipeline` on Pipelines
- Label `+ Credential` on Credentials
- Label `+ Toolkit` on Toolkits
- Label `+ Application` on Applications
- Label `+ MCP` on MCP
- Label `+ Artifact Bucket` on Artifacts

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar is in expanded state
- Any project selected

## Test Data

| Section | Expected Label |
|---|---|
| Chat | `+ Conversation` |
| Agents | `+ Agent` |
| Pipelines | `+ Pipeline` |
| Credentials | `+ Credential` |
| Toolkits | `+ Toolkit` |
| Applications | `+ Application` |
| MCP | `+ MCP` |
| Artifacts | `+ Artifact Bucket` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the left sidebar | Create button in the sidebar shows `+ Conversation` |
| 2 | Navigate to Agents | Create button updates to `+ Agent` |
| 3 | Navigate to Pipelines | Create button updates to `+ Pipeline` |
| 4 | Navigate to Credentials | Create button updates to `+ Credential` |
| 5 | Navigate to Toolkits | Create button updates to `+ Toolkit` |
| 6 | Navigate to Applications | Create button updates to `+ Application` |
| 7 | Navigate to MCP | Create button updates to `+ MCP` |
| 8 | Navigate to Artifacts | Create button updates to `+ Artifact Bucket` |

## Expected Final State

Create button updates to `+ Artifact Bucket`

## Pass/Fail Criteria

**Pass:**
- Each section shows exactly the correct label in the `+ [EntityName]` format
- Button is a split button (label part + `v` arrow part visible)

**Fail:**
- Any section shows the wrong entity name
- Button shows generic `+ Create` or only `+` instead of entity name
- Button reverts to a previous label when switching sections
