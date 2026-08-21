---
id: ELITEA-2684
title: "Tool Groups Render in Correct Fixed Order with All Required UI Elements"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, grouping, ui]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2684: Tool Groups Render in Correct Fixed Order with All Required UI Elements

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that tools are displayed under group headers in the exact order Read → Create & update → Delete → Execute, with correct badges, info icons, tooltips, and selected/total counts.

**Coverage:**
- Groups appear in fixed order: Read → Create & update → Delete → Execute
- Each group header displays label, badge, info icon, and selected/total count
- Info tooltips show correct text for each group
- Empty groups are hidden (verified across different toolkit types)
- Consistent behavior across GitHub, Jira, Artifact toolkits

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- At least one SDK toolkit with tools across all four groups exists (e.g., GitHub toolkit)
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page in Private project and open an existing SDK toolkit with tools across all four groups (e.g., GitHub toolkit). | Toolkit configuration page opens successfully. |
| 2 | Scroll to Tools section and verify group order from top to bottom. | Groups appear in exact order: **Read** → **Create & update** → **Delete** → **Execute**. |
| 3 | Inspect the **Read** group header. | Group label "Read" is displayed. "Read-only" badge is shown. ⓘ icon is present next to the label. Selected/total count is displayed (e.g., "4 / 26"). |
| 4 | Inspect the **Create & update** group header. | Group label "Create & update" is displayed. "Changes data" badge is shown. ⓘ icon is present. Selected/total count is displayed. |
| 5 | Inspect the **Delete** group header. | Group label "Delete" is displayed. "Destructive" badge is shown. ⓘ icon is present. Selected/total count is displayed. |
| 6 | Inspect the **Execute** group header. | Group label "Execute" is displayed. "Unrestricted" badge is shown. ⓘ icon is present. Selected/total count is displayed. |
| 7 | Hover over the ⓘ icon next to the **Read** group label. | Tooltip shows: "Returns data. Nothing is created, changed or destroyed." |
| 8 | Hover over the ⓘ icon next to the **Create & update** group label. | Tooltip shows: "Creates or modifies data in the target system." |
| 9 | Hover over the ⓘ icon next to the **Delete** group label. | Tooltip shows: "Destroys data. Not reversible from Elitea." |
| 10 | Hover over the ⓘ icon next to the **Execute** group label. | Tooltip shows: "Runs a caller-supplied query, script, pipeline or raw API call. Effect is not bounded by the tool." |
| 11 | Open a **Jira** toolkit and verify group order, badges, and tooltips. | Groups appear in correct order. Only **non-empty groups** are displayed (e.g., Delete/Execute may be hidden if no such tools). Badges and tooltips are correct for displayed groups. |
| 12 | Open an **Artifact** toolkit and verify group order, badges, and tooltips. | Groups appear in correct order. Only **non-empty groups** are displayed. Badges and tooltips are correct. |

## Expected Final State

Tool groups display correctly with proper UI elements across different toolkit types.

## Pass/Fail Criteria

**Pass:**
- Groups appear in fixed order: Read → Create & update → Delete → Execute
- Each group header displays: label, badge, info icon, selected/total count
- Badge designations are correct: Read-only, Changes data, Destructive, Unrestricted
- All four info tooltips show correct explanatory text
- Empty groups are hidden across all tested toolkit types
- Behavior is consistent across GitHub, Jira, Artifact toolkits

**Fail:**
- Groups appear in wrong order
- Any group header is missing label, badge, info icon, or count
- Badge text is incorrect for any group
- Tooltip text is missing or incorrect for any group
- Empty groups are displayed
- Behavior differs between toolkit types
