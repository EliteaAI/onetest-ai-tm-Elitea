---
id: ELITEA-1757
title: "Verify Context Management modal layout is correct with Bare persona"
priority: high
type: functional
module: ui
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, ui, layout]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1757: Verify Context Management modal layout is correct with Bare persona

**Module:** UI · **Priority:** High · **Type:** Functional

**Objective:** Verify that Context Management modal layout displays correctly with Bare persona selected

## Preconditions

- User is logged into EliteA platform
- User can access Context Management modal
- Bare personality is available in system

## Test Data

- Custom instructions: "Test custom instructions for layout verification"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Verify modal header displays "Context Management" or similar | Header visible and correct |
| 4 | Verify "Persona" section is present | Section labeled "Persona" visible |
| 5 | Verify personality dropdown is within Persona section | Dropdown visible with label "Personality" or similar |
| 6 | Select "Bare" from personality dropdown | Bare selected |
| 7 | Verify custom instructions field appears | Text field/area for custom instructions visible |
| 8 | Verify custom instructions field label | Label reads "Custom Instructions" or similar |
| 9 | Verify custom instructions field is editable | Field accepts text input |
| 10 | Enter test custom instructions | Text appears in field |
| 11 | Verify character counter (if present) | Counter updates as text entered |
| 12 | Verify field placeholder text (if any) | Placeholder provides helpful guidance |
| 13 | Check vertical spacing between elements | Spacing is adequate, not cramped |
| 14 | Verify other Context Management sections still visible | Context Budget, other controls present |
| 15 | Verify modal action buttons (Apply, Cancel, etc.) | Buttons visible and accessible |
| 16 | Test responsive layout on different screen sizes | Layout adapts appropriately |

## Expected Final State

- Context Management modal layout clean and organized
- Persona section clearly defined
- Personality dropdown and custom instructions field properly positioned
- All elements visible and accessible
- Layout responsive across screen sizes
- No visual bugs or overlapping elements

## Pass/Fail Criteria

**Pass:**
- Modal layout clean and professional
- All Bare personality UI elements present
- Custom instructions field visible and functional
- Proper spacing and alignment
- Responsive design works correctly
- No visual bugs or layout issues

**Fail:**
- Modal layout broken or disorganized
- Missing UI elements for Bare personality
- Custom instructions field not visible or broken
- Poor spacing, alignment, or overlapping elements
- Responsive design broken
- Visual bugs or layout errors
