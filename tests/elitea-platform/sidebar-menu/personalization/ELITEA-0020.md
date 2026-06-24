---
id: ELITEA-0020
title: Verify personality dropdown displays all 7 options in correct order
priority: high
type: functional
module: ui
status: approved
execution_type: manual
tags:
  - personality
  - ui
  - dropdown
  - display
requirements:
  - "#5394"
---

# Verify personality dropdown displays all 7 options in correct order

## Preconditions

- User is logged into EliteA platform
- User can access Context Management modal
- Personality dropdown is implemented and visible

## Test Data

- Expected personality options in order:
  1. Generic
  2. Bare
  3. QA
  4. Nerdy
  5. Quirky
  6. Cynical
  7. None

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Locate personality dropdown in Persona section | Dropdown visible and enabled |
| 4 | Click personality dropdown | Dropdown expands showing all options |
| 5 | Verify option 1: Generic | "Generic" displayed as first option |
| 6 | Verify option 2: Bare | "Bare" displayed as second option |
| 7 | Verify option 3: QA | "QA" displayed as third option |
| 8 | Verify option 4: Nerdy | "Nerdy" displayed as fourth option |
| 9 | Verify option 5: Quirky | "Quirky" displayed as fifth option |
| 10 | Verify option 6: Cynical | "Cynical" displayed as sixth option |
| 11 | Verify option 7: None | "None" displayed as seventh (last) option |
| 12 | Verify no additional options | Exactly 7 options, no more |
| 13 | Verify visual presentation | All options properly formatted, readable, aligned |
| 14 | Test dropdown on different screen sizes | Dropdown displays correctly on mobile, tablet, desktop |

## Expected Final State

- Personality dropdown displays exactly 7 options
- Options appear in specified order: Generic, Bare, QA, Nerdy, Quirky, Cynical, None
- All options visible and selectable
- Dropdown UI is clean and professional
- Responsive design works across screen sizes

## Pass/Fail Criteria

**Pass:**
- All 7 personality options displayed
- Options in correct order
- No missing or duplicate options
- Clean visual presentation
- Dropdown functional and accessible

**Fail:**
- Missing any personality option
- Options in wrong order
- Duplicate options appear
- Visual issues or formatting problems
- Dropdown broken or inaccessible
