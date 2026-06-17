---
id: ELITEA-0122
title: "Default and Custom Icon Display on Chipsets"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [nfr:usability, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3535]
---
# ELITEA-0122: Default and Custom Icon Display on Chipsets

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that chipsets show appropriate default icons when no custom icon is set, and show the custom icon when one is configured.

**Coverage:**
- Toolkit with custom icon: custom icon rendered in chipset
- Toolkit without custom icon: meaningful default/fallback icon shown (no broken image, empty space, or "?" placeholder)
- Default icons are visually distinct across entity types (LLM icon ≠ Toolkit icon ≠ Agent icon)
- Icons remain consistent after browser page reload

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Toolkit A: has a custom icon uploaded in its settings
- Toolkit B: has NO custom icon configured (icon field empty or default)
- An Agent uses both Toolkit A and Toolkit B
- Browser: Chrome/Edge latest

## Test Data

- Toolkit A: custom icon configured (note the icon before testing)
- Toolkit B: no custom icon set
- Agent: uses both Toolkit A and Toolkit B
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA. Navigate to Toolkits in the left sidebar. Open Toolkit A settings. Confirm a custom icon is uploaded and note what it looks like. | Toolkit A settings are open; a custom icon is visible and noted. |
| 2 | Navigate back to Toolkits and open Toolkit B settings. Confirm the icon field is empty or shows a default placeholder — no custom icon is set. | Toolkit B settings confirm no custom icon. |
| 3 | Navigate to Agents and open the agent using both toolkits. Switch to the Chat or Run tab. Enter a prompt that triggers actions from both Toolkit A and Toolkit B. Press Send. | Agent processes the prompt; tool calls from both toolkits are executed. |
| 4 | Wait for execution to complete. Open the thinking steps / execution trace panel. | Execution trace shows chipsets including entries for Toolkit A and Toolkit B. |
| 5 | Locate the chipset for Toolkit A (with custom icon). Look at the icon on the left side of the chipset label. | The icon shown matches the custom icon configured for Toolkit A in step 1 — not a generic default icon. |
| 6 | Locate the chipset for Toolkit B (no custom icon). Look at the icon on the left side of its label. | A meaningful fallback/default icon is displayed — no broken image (⚠️), empty square, or '?' shown. |
| 7 | Compare the default icon on Toolkit B to the icon on the LLM chipset and the Agent chipset (if visible in the trace). | Each entity type shows a visually distinct default icon — LLM icon, Toolkit icon, and Agent icon are different from one another. |
| 8 | Refresh the browser page (F5) and re-open the same execution trace run from History Runs. | Execution trace re-loads. |
| 9 | Verify Toolkit A still shows its custom icon and Toolkit B still shows the default icon after page reload. | Icons are consistent after reload — no icon reverts to a broken state. |

## Expected Final State

Icons are consistent after reload — no icon reverts to a broken state.

## Pass/Fail Criteria

**Pass:**
- Custom icon shown when configured on Toolkit A
- Meaningful default icon shown for Toolkit B (no broken image or placeholder)
- Different entity types have visually distinct default icons
- Icons remain correct after page reload

**Fail:**
- Broken image (⚠️), empty square, or "?" shown for any icon
- Custom icon is ignored and default shown instead
- All entity types share the same default icon (no visual distinction)
