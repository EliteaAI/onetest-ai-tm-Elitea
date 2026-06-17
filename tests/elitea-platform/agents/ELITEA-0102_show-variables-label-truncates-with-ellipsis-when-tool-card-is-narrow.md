---
id: ELITEA-0102
title: "\"Show variables\" Label Truncates with Ellipsis When Tool Card Is Narrow"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3833]
---
# ELITEA-0102: "Show variables" Label Truncates with Ellipsis When Tool Card Is Narrow

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the "Show variables" label text truncates with a CSS ellipsis rather than wrapping to a second line when the Tool Card is too narrow to display the full text.

**Coverage:**
- "Show variables" text does not wrap to a second line at narrow viewport widths
- Ellipsis (`...`) appears in the label when horizontal space is insufficient
- Variable count `(N)` remains visible on the same line as the truncated label
- At wider viewports the full "Show variables (N)" text is displayed without truncation
- Truncation applies equally to the "Hide variables" state after toggle

## Preconditions

- Logged in to elitea.ai
- Private project context selected
- A **child Agent** exists with **≥ 2 variables** defined in its instructions (e.g., `{{var1}}`, `{{var2}}`)
- A **parent Agent** (or Pipeline) exists that has the child Agent added in its TOOLKITS section as a nested agent — this causes the "Show variables (2)" toggle to appear on that Tool Card
- Browser: Chromium-based (Chrome or Edge), desktop

## Test Data

| Item | Value |
|---|---|
| Child Agent | Agent with variables `{{var1}}`, `{{var2}}` in its instructions |
| Parent Agent | Agent with the child Agent added as a nested sub-agent in TOOLKITS |
| Narrow viewport | 768 px |
| Medium viewport | 1024 px |
| Wide viewport | 1280 px |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open DevTools and set browser viewport width to 768 px. | Viewport is set to 768 px wide. |
| 2 | Navigate to the parent Agent's detail page. Open the TOOLKITS section. Locate the Tool Card for the nested child Agent. | The Tool Card for the nested child Agent is visible and displays the 'Show variables (2)' toggle label. |
| 3 | Inspect the 'Show variables (2)' toggle label text within the narrow card. | The text 'Show variables' is truncated with a visible ellipsis (e.g., 'Show var...') and does NOT wrap onto a second line. The count '(2)' is fully visible on the same line. |
| 4 | Click the 'Show variables (2)' toggle to expand the variables area. | Variables expand. The toggle label changes to 'Hide variables (2)' (or equivalent). The 'Hide variables' text is also truncated with ellipsis at 768 px — count '(2)' remains visible. |
| 5 | Set viewport width to 1024 px and observe the same Tool Card. | The full text 'Show variables (2)' or 'Hide variables (2)' is rendered without truncation or ellipsis. |
| 6 | Set viewport width to 1280 px and observe the same Tool Card. | The full text is rendered without truncation at 1280 px as well. |

## Expected Final State

The full text is rendered without truncation at 1280 px as well.

## Pass/Fail Criteria

**Pass:**
- At 768 px: label truncates with ellipsis, does NOT wrap, count (N) is fully visible
- At 1024 px and 1280 px: full label text rendered without ellipsis
- Truncation behavior applies to both "Show variables" and "Hide variables" states

**Fail:**
- Label wraps to a second line at any tested viewport width
- Count (N) is hidden, clipped, or pushed off-screen
- Ellipsis does not appear when the card is too narrow to display the full text
- Toggle fails to expand/collapse after the fix
