---
id: ELITEA-2640
title: "Participant Panel Rendering - No Regression for All Participant Types"
priority: low
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, participants, ui-regression, P2, share-chat]
requirements: [3837, EliteaAI/elitea_issues#7489]
---
# ELITEA-2640: Participant Panel Rendering - No Regression for All Participant Types

**Module:** Chat Interface · **Priority:** Low · **Type:** Functional

**Objective:** Verify that duplication does not regress participant rendering for Users, Agents, Pipelines, Toolkits, or MCPs in the participant panel.

## Preconditions

- User is logged in to {{base_url}}
- Chat exists with all participant types:
  - Users (multiple)
  - Agents
  - Pipelines
  - Toolkits
  - MCPs
- Participant panel displays correctly before duplication

## Test Data

- URL: {{base_url}}
- Comprehensive chat with:
  - 2+ Users
  - 1+ Agent
  - 1+ Pipeline
  - 1+ Toolkit
  - 1+ MCP

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open original chat with all participant types | Chat opens successfully |
| 2 | Open Participants panel | All participant sections visible |
| 3 | Verify the Users card ("Whole Team (N)" / "N users" / "Only You", " · 🔗 n" for the owner) and its users dropdown | Card and dropdown rendered properly |
| 4 | Verify AGENTS section displays agent icons/names correctly | Agents rendered properly |
| 5 | Verify PIPELINES section displays pipeline icons/names | Pipelines rendered properly |
| 6 | Verify TOOLKITS section displays toolkit icons/names | Toolkits rendered properly |
| 7 | Verify MCPS section displays MCP icons/names/status | MCPs rendered properly |
| 8 | Document current rendering (screenshots if possible) | Reference state captured |
| 9 | Duplicate the chat | Duplicate created |
| 10 | Open duplicated chat and open Participants panel | Participants panel opens |
| 11 | Verify the Users card shows the access of the duplicate (not the external links of the original) | Rendered correctly; no layout issues |
| 12 | Verify AGENTS section renders identically | No visual regression |
| 13 | Verify PIPELINES section renders identically | No visual regression |
| 14 | Verify TOOLKITS section renders identically | No visual regression |
| 15 | Verify MCPS section renders identically | No visual regression |
| 16 | Check for any layout issues, overlaps, or missing elements | No UI defects |
| 17 | Collapse the Participants panel and hover each icon | Badges correct; tooltips open to the left |

## Expected Final State

- All participant types render correctly in duplicate
- No visual regression from original
- Icons, names, status indicators all display properly
- Layout consistent and clean
- No rendering errors

## Pass/Fail Criteria

**Pass:**
- All participant types render correctly
- Visual consistency with original
- No layout issues or overlaps
- Icons and names display properly
- Status indicators functional
- No UI regression

**Fail:**
- Any participant type fails to render
- Visual differences from original
- Layout broken or overlapping elements
- Missing icons or names
- Status indicators broken
- UI defects introduced
