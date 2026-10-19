---
id: ELITEA-4121
title: "Verify expanding welcome message/description via show-more does not modify agent data"
priority: critical
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}` with permissions to create, edit, and publish agents
- A published agent exists with a welcome message long enough to require "Show more"

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents-studio` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In the agent editor, note the current welcome message, description, and character counts for the test agent | Values recorded |
| 2 | In Agents Studio, open the agent's card and click "Show more" to expand the welcome message | Full text is displayed |
| 3 | Close/collapse the expanded view | Card returns to clamped state |
| 4 | Reload the Agents Studio page | Page reloads without errors |
| 5 | Re-open the agent in the editor | Editor loads the agent |
| 6 | Compare welcome message/description text and character counts to the values recorded in step 1 | Values are identical |
| 7 | Check for any "unsaved changes" indicator, version increment, or edit-history/audit entry | No such indicator or entry exists as a result of steps 2–3 |

## Expected Final State

Agent data (welcome message, description, version) is unchanged; no save, version, or history side effects were recorded from viewing the expanded text.

## Pass/Fail Criteria

**Pass:**
- Text and character counts are identical before and after expand/collapse
- No unsaved-changes prompt, version bump, or history entry is generated

**Fail:**
- Any difference in text or character count is observed
- Any save/version/history side effect is triggered merely by expanding/collapsing the view
