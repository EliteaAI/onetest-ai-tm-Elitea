---
id: ELITEA-1910
title: "Build with AI — Suggested Skills section is shown with up to 5 skills"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1910: Build with AI — Suggested Skills section is shown with up to 5 skills

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the review form displays a "Suggested Skills" section with up to 5 unselected Skill cards, each showing the skill name and description.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- At least one Skill exists in the project that could be suggested.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "An agent that formats code reviews and writes PR summaries" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft that would benefit from Skills (e.g., "An agent that formats code reviews and writes PR summaries") | The modal shows a loading state then transitions to the review form |
| 2 | Wait for generation to complete | The review/edit form is displayed |
| 3 | Verify a "SUGGESTED SKILLS" section is displayed in the review form | The "SUGGESTED SKILLS" section is present on the review form |
| 4 | Verify at most 5 Skill cards are shown | The section displays between 1 and 5 Skill cards (never more than 5) |
| 5 | Verify each Skill card shows Skill name and Skill description | Each Skill card displays the skill name and a description |
| 6 | Verify all suggested Skills are unselected by default | All Skill cards appear in an unselected state, requiring explicit user action to select |

---

## Expected Final State

The review form shows a "SUGGESTED SKILLS" section with up to 5 Skill cards, each displaying name and description, all unselected by default.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The SUGGESTED SKILLS section is present with 1–5 unselected skill cards, each showing name and description.

**Fail:**
- Any step produces an error or unexpected result.
- The section is absent, more than 5 skills are shown, or any skill is pre-selected.
