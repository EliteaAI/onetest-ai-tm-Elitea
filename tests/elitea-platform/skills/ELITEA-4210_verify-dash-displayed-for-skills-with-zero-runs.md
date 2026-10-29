---
id: ELITEA-4210
title: "Verify '—' displayed for skills with 0 runs in AVG LATENCY, TOKENS, COST columns"
priority: high
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8, nfr:usability]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one skill exists with 0 runs but has agent/chat uses (used only via `~skill` in chat)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Skill | Any existing skill |
| Chat | New chat with only a model (no agent) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Create a new chat with only a model (no agent) | Chat opens successfully |
| 2 | Type `~<skill-name>` and send a message | Skill is invoked in chat |
| 3 | Wait for skill response | Skill responds in chat |
| 4 | Navigate to Settings → Analytics → Skills | Skills analytics page loads |
| 5 | Find the skill used in step 2 in Skill Activity table | Skill appears in the table |
| 6 | Check RUNS column for this skill | Shows: 0 |
| 7 | Check AGENT & CHAT USES column | Shows: 1 (or higher) |
| 8 | Check AGENTS USING column | Shows: 0 |
| 9 | Check AVG LATENCY column | Shows: "—" (not "0ms") |
| 10 | Check TOKENS column | Shows: "—" (not "0") |
| 11 | Check COST column | Shows: "—" (not "$0.00") |
| 12 | Hover over AGENT & CHAT USES tooltip | Tooltip explains: "Uses add no tokens or cost here; that cost is on the agent or chat." |
| 13 | Check ERRORS column | Shows: 0 |
| 14 | Check LAST USED column | Shows recent timestamp |

## Expected Final State

Skills with 0 runs display "—" instead of zero values (0ms, 0, $0.00) in AVG LATENCY, TOKENS, and COST columns. This correctly indicates that the skill was used inside an agent/chat but not run directly, so these metrics don't apply.

## Pass/Fail Criteria

**Pass:**
- Skills with 0 runs display "—" in AVG LATENCY, TOKENS, and COST columns
- RUNS, AGENT & CHAT USES, AGENTS USING, USERS columns show numeric values
- Display correctly indicates skill was used but not run directly
- "—" is consistent across all three columns (AVG LATENCY, TOKENS, COST)

**Fail:**
- Shows "0ms", "0", or "$0.00" instead of "—"
- "—" appears in columns that should show numeric values
- Inconsistent use of "—" across the three columns
