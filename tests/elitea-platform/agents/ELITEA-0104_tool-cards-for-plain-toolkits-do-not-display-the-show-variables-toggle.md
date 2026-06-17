---
id: ELITEA-0104
title: "Tool Cards for Plain Toolkits Do Not Display the \"Show Variables\" Toggle"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3833]
---
# ELITEA-0104: Tool Cards for Plain Toolkits Do Not Display the "Show Variables" Toggle

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the fix does not regressively add a "Show variables" toggle to Tool Cards for plain toolkits that have no variables, and that no ghost UI element appears in the variables row area on such cards.

**Coverage:**
- Plain toolkits (e.g., Artifacts) with no variable placeholders show no "Show variables" toggle
- Only expected controls are present: toolkit name, "Show tools / Hide tools", open-in-new-tab, delete
- No empty/ghost variables row renders due to the height increase
- Behavior is consistent at both wide (1280 px) and narrow (768 px) viewports

## Preconditions

- Logged in to elitea.ai
- Private project context selected
- A **parent Agent** exists that has a **plain Artifacts toolkit** attached in TOOLKITS — this toolkit has no variables defined, so the "Show variables" toggle should not appear
- Browser: Chromium-based, desktop

## Test Data

| Item | Value |
|---|---|
| Parent Agent | Any agent with the Artifacts toolkit in TOOLKITS |
| Toolkit to inspect | Artifacts (no variables) |
| Viewport widths | 1280 px (default), 768 px (narrow) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the parent Agent's detail page. Open the TOOLKITS section. Locate the Artifacts Tool Card. | The Artifacts Tool Card is visible. |
| 2 | Inspect the Artifacts Tool Card for the presence of a 'Show variables' or 'Hide variables' toggle. | No 'Show variables' or 'Hide variables' toggle is present. Only the toolkit name, 'Show tools / Hide tools' toggle, open-in-new-tab, and delete button are visible. |
| 3 | Inspect the card area where a variables row would appear (below the toolkit name row). Check for any empty row, extra whitespace, or ghost DOM element. | No empty variables row, extra spacing, or invisible DOM element occupies the variables row area. |
| 4 | Set viewport width to 768 px and repeat the inspection of the Artifacts Tool Card. | At narrow viewport, still no 'Show variables' toggle appears. No ghost element is visible. All card controls remain fully accessible. |
| 5 | Click 'Show tools' on the Artifacts card and verify the tools list expands normally. | Tools list expands correctly. The variables toggle row does not appear after expanding tools. |

## Expected Final State

Tools list expands correctly. The variables toggle row does not appear after expanding tools.

## Pass/Fail Criteria

**Pass:**
- No "Show variables" toggle present on the Artifacts Tool Card at any viewport width
- No ghost element, empty row, or unexplained whitespace in the variables row area
- "Show tools / Hide tools" and all standard card controls work normally

**Fail:**
- "Show variables" toggle appears on a plain toolkit card with no variables
- Ghost DOM element or empty row appears in the variables area
- Standard card controls are missing or broken on the plain toolkit card
