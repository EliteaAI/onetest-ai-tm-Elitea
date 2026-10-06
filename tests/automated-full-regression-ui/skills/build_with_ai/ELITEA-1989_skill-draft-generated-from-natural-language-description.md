---
id: ELITEA-1989
title: "Skill draft is generated from a natural-language description"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-1989: Skill draft is generated from a natural-language description

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that submitting a natural-language description in the Build with AI modal triggers skill draft generation, shows a loading state, and produces a review form with Name, Description, and Instructions fields — without any suggested tools, agents, pipelines, toolkits, MCPs, or resources.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The Build with AI modal is accessible from the New Skill creation screen.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language description | "A skill that helps write concise GitHub PR review comments" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Build with AI modal | The modal opens with the prompt input field visible |
| 2 | Enter a clear natural-language description: "A skill that helps write concise GitHub PR review comments" | The input field accepts and displays the entered description |
| 3 | Click "Generate" | Generation is initiated |
| 4 | Verify the modal shows a loading state with text "Generating skill draft..." | The modal displays the loading state and "Generating skill draft..." text |
| 5 | Wait for generation to complete | Generation completes and the modal transitions |
| 6 | Verify the modal transitions to a review/edit form showing generated: Name, Description, Instructions | The review/edit form is shown with generated Name, Description, and Instructions fields populated |
| 7 | Verify no suggested tools, agents, pipelines, toolkits, MCPs, or resources section is shown | No suggested tools, agents, pipelines, toolkits, MCPs, or resources are displayed |

---

## Expected Final State

The modal shows a review/edit form with generated Name, Description, and Instructions pre-filled, and no additional sections (tools, agents, pipelines, etc.) are present.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Generation completes and the review form shows Name, Description, and Instructions with no extra sections.

**Fail:**
- Any step produces an error or unexpected result.
- The draft is not generated, fields are empty, or forbidden sections (tools, agents, etc.) appear.
