---
id: ELITEA-0953
title: "Enable Toggle Controls Project Context Injection"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, enable-toggle, feat:settings, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0953: Enable Toggle Controls Project Context Injection

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Enable Project Context toggle correctly enables and disables context injection, and that toggle state is per-project.

**Coverage:**
- Toggle ON injects context into agent execution
- Toggle OFF stops injection
- Toggle state persists
- Toggle is independent per project

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Copper phoenix rises at noon`
- Two different projects (Project A and Project B)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context content to 'QA-TEST-PHRASE: Copper phoenix rises at noon'. Set Enable toggle = ON. Save. | Content and toggle state saved. |
| 2 | Open an agent on the Agent page. Ask: 'What is the QA-TEST-PHRASE?' | Agent returns: 'Copper phoenix rises at noon'. |
| 3 | Navigate to Project Context settings. Set Enable toggle = OFF. Save. Run the same agent again with the same question. | Agent does NOT return the phrase. Context is not injected. |
| 4 | Reload the settings page. | Toggle state remains OFF after reload. |
| 5 | Enable toggle in Project A. Navigate to Project B and check its toggle state. | Project B toggle is unaffected — toggle states are independent per project. |

## Expected Final State

Project B toggle is unaffected — toggle states are independent per project.

## Pass/Fail Criteria

**Pass:**
- Agent returns phrase when toggle is ON
- Agent does not return phrase when toggle is OFF
- Toggle state persists after reload
- Projects have independent toggle states

**Fail:**
- Toggle OFF still injects context
- Toggle state resets on reload
- One project's toggle affects another
