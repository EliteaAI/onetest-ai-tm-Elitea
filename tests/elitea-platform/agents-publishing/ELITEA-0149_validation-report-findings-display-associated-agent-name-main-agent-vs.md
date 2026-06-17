---
id: ELITEA-0149
title: "Validation Report Findings Display Associated Agent Name (Main Agent vs Sub-Agent)"
priority: critical
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [story:4049, story:3774, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4432, EliteaAI/elitea_issues#4162, EliteaAI/elitea_issues#4516]
---
# ELITEA-0149: Validation Report Findings Display Associated Agent Name (Main Agent vs Sub-Agent)

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that each finding in the Publish Validation Report clearly displays the name of the agent it belongs to — either "Main Agent" (when the backend `context` field is null) or the specific sub-agent name (when `context` is populated) — so users know exactly what needs to be fixed.

**Coverage:**
- Findings scoped to the parent agent are labeled with the main agent name or "Main Agent"
- Findings scoped to a sub-agent are labeled with the sub-agent's name
- The label is visible on each finding item (Critical, Warning, Suggestion) in the validation results
- Without the fix, all findings appear without any agent attribution — users cannot tell which component is affected

## Preconditions

- Logged in to {{base_url}} as a user with publishing rights
- A parent agent exists with a sub-agent attached
- Both the parent agent and the sub-agent have known validation violations (e.g., generic name, abstract description) to ensure findings appear for both in the report

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a parent agent with a sub-agent attached. Configure both to produce validation findings:  Parent agent: - Name: generic value, e.g. 'Assistant' (warning: too generic) - Description: absent or one word (warning: missing / too abstract)  Sub-agent: - Name: generic value, e.g. 'Bot' (warning: too generic) - Description: absent or one word (warning: missing / too abstract)  Click Publish, enter a version name, accept the terms, and click Continue to trigger AI validation. | Validation runs and the report displays findings for both the parent agent and the sub-agent. |
| 2 | Review the validation findings list in the report. For each finding, check whether an agent name label is displayed (e.g., next to the field name, finding title, or as a badge/prefix). | Every finding is labeled with the agent it belongs to: - Findings for the parent agent display the main agent's name or 'Main Agent' - Findings for the sub-agent display the sub-agent's exact name (e.g., 'Bot')  No finding appears without an attribution label — it is always clear which agent the issue belongs to. |
| 3 | Expand the Summary Details popup (if available). Review each listed finding item (Critical, Warning, Suggestion) in the popup. | Each finding item in the Summary Details popup also shows the associated agent name, consistent with the main report view. Main agent findings show main agent name; sub-agent findings show the sub-agent's name. |
| 4 | Publish a second agent that has NO sub-agent attached (standalone agent) with one known violation. Trigger validation and review the findings. | Findings for a standalone agent are attributed to the main agent only. No sub-agent labels appear. |

## Expected Final State

Findings for a standalone agent are attributed to the main agent only. No sub-agent labels appear.

## Pass/Fail Criteria

**Pass:**
- Each validation finding clearly displays the name of the agent it applies to (main agent or sub-agent name)
- Main agent findings are attributed to the main agent (not blank or labeled as a sub-agent)
- Sub-agent findings are attributed using the sub-agent's exact name (not blank or labeled as main agent)

**Fail:**
- Any finding appears without an agent name label
- All findings are shown without attribution — user cannot tell which agent the issue belongs to
- Sub-agent name is missing from sub-agent-scoped findings
- Main agent findings are incorrectly labeled with a sub-agent name or vice versa
