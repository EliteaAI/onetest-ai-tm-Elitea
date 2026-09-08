---
id: ELITEA-1899
title: "Agent icon can be changed and persists on the agents list card"
priority: low
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_icon_management.TestAgentIconManagement.test_agent_icon_change_persists_on_list_card
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/567
sanctioned_red: "#2055"
---

# ELITEA-1899: Agent icon can be changed and persists on the agents list card

**Module:** agents · **Priority:** low · **Type:** functional

**Objective:** Verify that an agent's icon can be changed via the icon picker, that the new icon is shown immediately in the agent header, and that it persists on the agents list card (icon persists independently via immediate PUT request, not through form Save).

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Click the agent icon near the agent name — verify an icon picker opens | The icon picker dialog opens |
| 3 | Select a different icon from the picker | The new icon is selected |
| 4 | Verify the new icon is shown in the agent header immediately | The agent header displays the newly selected icon |
| 5 | Verify the Save button remains disabled (icon persists independently) | The Save button remains **disabled** after the icon-only change. The icon change persists **independently** via the immediate PUT request from Step 3. The icon field is NOT part of the form's tracked draft state. |
| 6 | Navigate to the Agents dashboard | The Agents dashboard loads |
| 7 | Verify the agent card shows the newly selected icon | The agent's card on the dashboard displays the new icon |

**Note on Step 5:** Icon changes persist immediately via `PUT /api/v2/elitea_core/upload_icon/prompt_lib/{project}/{versionId}` and do not require clicking the main Save button. The icon field has its own independent persistence mechanism separate from the agent form's Save/Discard workflow. This is intentional UX behavior. (Updated 2026-07-22, resolves issue #566)

---

## Expected Final State

The newly selected icon is visible on the agent's card in the Agents dashboard, confirming persistence after save.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The new icon is displayed immediately in the header and persists on the agents list card.

**Fail:**
- Any step produces an error or unexpected result.
- The icon does not change, does not appear immediately, or reverts to the old icon on the dashboard.
