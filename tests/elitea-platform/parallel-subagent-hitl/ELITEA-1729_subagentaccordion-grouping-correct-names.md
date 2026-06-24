---
id: ELITEA-1729
title: "Parallel HITL approval cards grouped inside SubAgentAccordion with correct sub-agent names auto-expanded"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1729: Approval Cards Grouped Inside SubAgentAccordion

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in **In-Process mode (Track 1)**, when two parallel sub-agents are paused for HITL (aggregate interrupt), their approval cards are grouped inside named SubAgentAccordion sections that are auto-expanded.

**Behavior note:** In In-Process mode, the aggregate interrupt surfaces all pending HITL cards together. Each child's card should be visually grouped inside its own SubAgentAccordion with the sub-agent's name as header. This grouping helps users identify which approval belongs to which sub-agent.

## Preconditions

- Logged in to {{base_url}}
- **Execution mode: In-Process (Track 1)** — `parallel_subagent_dispatch` flag absent or `false`
- Parent agent with two named Application sub-agent tools (e.g., "Research Agent", "Action Agent")
- Both sub-agents have sensitive tools and are triggered in one parallel turn

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering both sub-agents in parallel, both pause for HITL | Both sub-agents paused |
| 2 | Observe chat UI accordion structure | Each sub-agent's card is inside its own labeled SubAgentAccordion section |
| 3 | Verify accordion headers | Headers display correct sub-agent names |
| 4 | Verify accordion expansion state | Both accordions auto-expanded — cards immediately visible without manual click |
| 5 | Verify card-to-sub-agent mapping | Each card's tool matches the correct sub-agent |

## Expected Final State

Two SubAgentAccordion sections visible, auto-expanded, correctly labeled, each containing its own correctly attributed card.

## Pass/Fail Criteria

**Pass:**
- Cards inside named accordions
- Headers show correct sub-agent names
- Accordions auto-expanded
- Correct tool-to-sub-agent mapping

**Fail:**
- Cards flat/ungrouped
- Wrong or generic headers
- Accordions collapsed (require manual click)
- Wrong tool attribution
