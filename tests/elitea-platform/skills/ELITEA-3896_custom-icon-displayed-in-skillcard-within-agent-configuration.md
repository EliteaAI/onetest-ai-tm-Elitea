---
id: ELITEA-3896
title: "Custom icon displayed in skillcard within agent configuration panel"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- At least one Skill with a distinctive custom icon exists
- At least one Agent exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Skill | Skill with custom icon |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or verify a Skill has a distinctive custom icon | Skill with custom icon exists |
| 2 | Navigate to Agents page | Agents page loads |
| 3 | Open an existing Agent for editing | Agent edit form loads |
| 4 | Scroll to the **SKILLS** accordion section | SKILLS section is visible |
| 5 | Click **+ Skill** to open the skill picker | SkillMenu dropdown opens |
| 6 | Select and attach the Skill with the custom icon | Skill is attached |
| 7 | Verify the SkillCard in the SKILLS section displays the custom icon | Custom icon is shown, not default `skill-icon.svg` |
| 8 | Click **Save** to save the Agent | Agent saves successfully |
| 9 | Re-open the Agent configuration | Agent edit form loads |
| 10 | Verify the custom icon still displays on the SkillCard | Custom icon persists |

## Expected Final State

The SkillCard within the Agent's SKILLS configuration section displays the custom icon for attached Skills that have one.

## Pass/Fail Criteria

**Pass:**
- Custom icon displays in SkillCard
- Icon persists after Agent save
- Icon persists after re-opening Agent

**Fail:**
- Default SVG icon shown instead of custom icon
- Icon not displayed after save
- Icon changes after re-opening
