---
id: ELITEA-0943
title: "Admin and Editor Can Configure Ignore Project Context Toggle on Agents"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, ignore-toggle, feat:settings, permissions, editor-role, story:3395, r-2.0.4, admin]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0943: Admin and Editor Can Configure Ignore Project Context Toggle on Agents

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that both Admin and Editor roles can configure the Ignore Project Context toggle on agents, while Viewer cannot.

**Coverage:**
- Editor can set Ignore toggle in Private project
- Admin and Editor can set Ignore toggle in Team project
- Viewer cannot set the toggle in any project

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: Purple heron rests at dawn`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: Purple heron rests at dawn'. Enable toggle = ON. Save. | Content and toggle saved. |
| 2 | Log in as Editor. Open an agent in the Private project on the Agent page → Advanced. Set 'Ignore Project Context' = ON. Save. | Save succeeds. No permission error. |
| 3 | Run the agent from the Agent page. Ask: 'What is the QA-TEST-PHRASE?' | Agent does NOT return the phrase. |
| 4 | Toggle Ignore = OFF. Save. Run agent again. | Agent returns the phrase again. |
| 5 | Log in as Admin. Open an agent in the Team project → Advanced. Set 'Ignore Project Context' = ON. Save. | Save succeeds. |
| 6 | Run the agent from the Agent page. Ask the same question. | Agent does NOT return the phrase. |
| 7 | Log in as Editor in the Team project. Perform same toggle test on an agent. | Editor can also set and save the toggle in Team project. |
| 8 | Log in as Viewer. Navigate to any agent → Advanced. | 'Ignore Project Context' toggle is read-only or not clickable for Viewer. |

## Expected Final State

'Ignore Project Context' toggle is read-only or not clickable for Viewer.

## Pass/Fail Criteria

**Pass:**
- Editor saves Ignore=ON in Private project; agent stops returning phrase
- Admin saves Ignore=ON in Team project; agent stops returning phrase
- Editor also works in Team project
- Viewer cannot save any change to the toggle

**Fail:**
- Editor blocked from setting toggle in Private project
- Viewer can set the toggle
