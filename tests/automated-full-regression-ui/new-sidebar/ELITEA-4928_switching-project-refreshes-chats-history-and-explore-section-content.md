---
id: ELITEA-4928
title: "Switching project refreshes Chats history and Explore section content"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4928: Switching project refreshes Chats history and Explore section content

## Preconditions

- User is logged in to `{{base_url}}`
- User has two projects (A and B) with different chats and different agents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Projects | Project A (private); Project B (team) |
| Section | Explore → Agents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select Project A in the project selector | The Chats history shows Project A's chats and folders |
| 2 | Switch to Project B | The Chats history refreshes and shows only Project B's chats and folders |
| 3 | Open **Explore → Agents** | The Agents page shows Project B's agents |
| 4 | Switch back to Project A while the Agents page is open | Both the Chats history and the Agents page show Project A's content |
| 5 | Click a chat in the history | The chat opens in Project A |

## Expected Final State

The sidebar and the open section page always reflect the selected project.

## Pass/Fail Criteria

**Pass:**
- History and section content match the selected project after every switch

**Fail:**
- Stale chats from the previous project remain, or content from the wrong project is shown

## Notes

**Source functional tests:** ELITEA-4903
**Regression rationale:** The chat history now lives in a shared sidebar, so wrong-project data would be shown across every page.
**Selected checkpoints:** History refresh on switch; section content refresh; chat opens in the selected project.
