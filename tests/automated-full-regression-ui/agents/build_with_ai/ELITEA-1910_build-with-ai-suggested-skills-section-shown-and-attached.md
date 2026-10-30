---
id: ELITEA-1910
title: "Build with AI — suggested skills section is shown and selected skills are attached to created agent"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1910: Build with AI — suggested skills section is shown and selected skills are attached to created agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the generated agent draft includes a "Suggested Skills" section showing up to 5 skills, and that explicitly selected skills are successfully attached to the created agent.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- At least one Skill exists in the project.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | Agent description that matches existing project skills (e.g., "research assistant with documentation skills") |
| Existing Skills | At least one Skill pre-existing in the project |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and enter a natural-language description that matches existing skills | The description is entered successfully |
| 2 | Click "Generate agent" | The generation process starts and completes |
| 3 | Verify the review form displays a "Suggested Skills" section | The "Suggested Skills" section is visible in the review form |
| 4 | Verify the section shows up to 5 suggested skills (if relevant matches exist) | Up to 5 skill cards are displayed in the section |
| 5 | Select one or more suggested skills by clicking them | Selected skill cards are highlighted as selected |
| 6 | Click "Approve" / "Create Agent" | The agent creation is initiated |
| 7 | Open the created Agent | The Agent detail page is displayed |
| 8 | Verify the selected skills are present in the SKILLS section of the created agent | The explicitly selected skills appear in the agent's SKILLS section |
| 9 | Verify any skills that were NOT selected are absent | Non-selected suggested skills are not attached to the agent |

---

## Expected Final State

The "Suggested Skills" section displays up to 5 relevant skills during agent draft review, and only explicitly selected skills are attached to the created agent.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The "Suggested Skills" section is visible and shows up to 5 skills.
- Selected skills are successfully attached to the created agent.
- Non-selected skills are not attached.

**Fail:**
- Any step produces an error or unexpected result.
- The "Suggested Skills" section is missing.
- The section displays more than 5 skills.
- Selected skills are not attached, or non-selected skills are incorrectly attached.

---

## Notes

**Source functional tests:** ELITEA-1910 (original), ELITEA-1911 (original)  
**Regression rationale:** Consolidated test verifying both the presence/display of the Suggested Skills section (up to 5 skills) and the successful attachment of selected skills to the created agent. Both assertions are sequential steps in the same user journey.  
**Selected checkpoints:** Section visibility, skill count limit, selection interaction, attachment verification.
