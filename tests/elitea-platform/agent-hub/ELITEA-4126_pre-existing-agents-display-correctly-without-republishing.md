---
id: ELITEA-4126
title: "Verify pre-existing published agents display correctly with new truncation/expand behavior without republishing"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- An agent published before this enhancement (PR EliteaAI/EliteaUI#1177) was deployed exists, with a welcome message exceeding the 8-line clamp. If unavailable in the test environment, note this as a known limitation and use the oldest available long-welcome-message agent as a best-effort substitute.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents-studio` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Without editing or republishing the pre-existing agent, open Agents Studio and locate its card | Card is visible |
| 2 | Verify the truncation indicator and "Show more" control appear | Control appears exactly as for newly published agents |
| 3 | Click "Show more" | Full welcome message text displays correctly and matches the agent's actual saved content |

## Expected Final State

Pre-existing published agents gain the new show-more/expand behavior automatically, without requiring any republish action.

## Pass/Fail Criteria

**Pass:**
- Show-more control and expansion work correctly for a pre-existing published agent without any edit/republish

**Fail:**
- Pre-existing published agent does not show the control, or expansion fails or shows incorrect text
