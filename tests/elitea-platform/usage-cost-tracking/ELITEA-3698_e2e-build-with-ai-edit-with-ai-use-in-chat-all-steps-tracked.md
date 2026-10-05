---
id: ELITEA-3698
title: "E2E: Build-with-AI → Edit-with-AI → use agent in Chat — all three steps tracked distinctly with correct per-model costs"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, integration, e2e, build-with-ai, edit-with-ai]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607", "EliteaAI/elitea_issues#6574"]
---

# ELITEA-3698: E2E: Build-with-AI → Edit-with-AI → use agent in Chat — all three steps tracked distinctly with correct per-model costs

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify the full journey of creating an agent with Build-with-AI, modifying it with Edit-with-AI before publishing, then using the resulting agent in a normal chat conversation, records three distinct `usage_event` entries (one per step) with correct per-model costs — no step's spend goes missing or gets merged with another's.

---

## Preconditions

- Logged in to {{base_url}} with permission to create and edit agents, and to use agents in Chat.

---

## Test Data

| Field | Value |
|-------|-------|
| Build description | "A travel-planning assistant" |
| Edit request | "Add a chat starter asking for the destination city" |
| Chat message | "Plan a 3-day trip to Lisbon" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Use Build-with-AI with the test description to create a new agent draft, then create the agent. | Agent is created; a `usage_event` row is produced for this call. |
| 2 | Record this row's tokens/cost (Row 1). | Row 1 captured for comparison. |
| 3 | Before publishing, use Edit-with-AI with the test edit request on the newly created agent. | Edit is applied; a separate `usage_event` row is produced for this call. |
| 4 | Record this row's tokens/cost (Row 2). | Row 2 captured; confirm it is distinct from Row 1 (different timestamp/id, not merged). |
| 5 | Use the resulting agent in a normal Chat conversation, sending the test chat message. | Agent responds in chat; a `usage_event` row is produced for this call (`event_type` consistent with chat/agent predict). |
| 6 | Record this row's tokens/cost (Row 3). | Row 3 captured; confirm it is distinct from Rows 1 and 2. |
| 7 | Review Analytics (e.g. Costs tab, "Total by Agent") for this agent. | All three rows' costs are visible and attributed correctly per model; no step's spend is missing from the agent's total. |

---

## Expected Final State

Three distinct `usage_event` rows exist (build, edit, chat-use), each with correct, non-overlapping cost attribution, summing correctly in the agent's Analytics total.

---

## Pass/Fail Criteria

**Pass:**
- Exactly three distinct rows exist for the three steps.
- Each row's cost is correct and the agent's Analytics total reflects the sum of all three.

**Fail:**
- Any step's row is missing.
- Two steps' usage is merged into a single row, or the agent's Analytics total omits one step's spend.
