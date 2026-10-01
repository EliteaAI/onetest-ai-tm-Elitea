---
id: ELITEA-3604
title: "Chat – Trigger differentiation: # shows all agents, & shows only private, + shows only users"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
automation_test_id: []
tags: [automated:UI:regression, feat:chat, feat:agents, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6368]
---

# ELITEA-3604: Chat – Trigger differentiation: # shows all agents, & shows only private, + shows only users

**Module:** chat-interface · **Priority:** high · **Type:** regression

**Objective:** Verify that different trigger characters show the correct entity types: `#` shows all agents/pipelines (including public), `&` shows only private agents, `+` shows only users.

---

## Preconditions

- User is logged in to the Elitea platform in a Team project.
- A conversation is open with:
  - 1 private agent added (e.g., "MyAgent")
  - 1 public agent from Agent Hub added (e.g., "PublicBot")
  - 2 users as participants (e.g., "Alice", "Bob")

---

## Test Data

| Field | Value |
|-------|-------|
| Private Agent | "MyAgent" |
| Public Agent | "PublicBot" (from Agent Hub) |
| User 1 | "Alice" |
| User 2 | "Bob" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Verify PARTICIPANTS panel shows: MyAgent, PublicBot in AGENTS; Alice, Bob in USERS | All participants visible |
| 2 | Type `#` in message input | "SEARCH RESULTS" dropdown appears showing ALL agents/pipelines including public ones from Agent Hub |
| 3 | Verify "MyAgent" AND "PublicBot" are both visible in # dropdown | Both private and public agents shown |
| 4 | Press ESC to close dropdown | Dropdown closes |
| 5 | Type `&` in message input | Private participant dropdown appears |
| 6 | Verify dropdown shows ONLY "MyAgent" | Only private agent shown |
| 7 | Verify "PublicBot" is NOT shown in & dropdown | Public agent from Agent Hub is excluded |
| 8 | Press ESC to close dropdown | Dropdown closes |
| 9 | Type `+` in message input | User mention dropdown appears |
| 10 | Verify dropdown shows ONLY users "Alice", "Bob" | Only users shown, NO agents |
| 11 | Verify NO agents (MyAgent, PublicBot) appear in + dropdown | Agents are excluded from user mention |

---

## Expected Final State

Each trigger character shows the correct entity type:
- `#` → ALL agents/pipelines (private + public from Agent Hub)
- `&` → ONLY private agents (excludes public)
- `+` → ONLY users (excludes all agents)

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- # shows all agents including public
- & shows only private agents, excludes public
- + shows only users, excludes all agents
- Each trigger opens a distinct dropdown with correct entities

**Fail:**
- Any step produces an error or unexpected result.
- Triggers show overlapping/incorrect entity types
- & shows public agents
- + shows agents
