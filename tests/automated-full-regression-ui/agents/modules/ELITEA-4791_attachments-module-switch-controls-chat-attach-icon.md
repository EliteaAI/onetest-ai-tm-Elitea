---
id: ELITEA-4791
title: "Attachments module switch in the Modules dropdown controls the agent chat attach icon and file attachment"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents, nfr:ui, modules, attachments, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4791: Attachments module switch in the Modules dropdown controls the agent chat attach icon and file attachment

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that switching Attachments ON in the "+ Modules" dropdown enables the chat attach icon so files can be attached, and switching it OFF disables the icon and shows an error message on an attach attempt.

## Preconditions

- Logged in to `{{base_url}}`
- An editable Agent exists
- Attachments module is available on the environment
- Browser: Chrome (latest)

## Test Data

| Field | Value |
|---|---|
| File | `sample.txt` (< 1 KB, plain text) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent, click "+ Modules", switch Attachments ON and click Save | Agent is saved with Attachments ON |
| 2 | Open the Agent chat panel | Attach icon is displayed and enabled |
| 3 | Attach `sample.txt` and send "Summarize the attached file" | File is attached and sent; Agent replies with content based on the file |
| 4 | Click "+ Modules", switch Attachments OFF and click Save | Agent is saved with Attachments OFF |
| 5 | Open the Agent chat panel | Attach icon is disabled |
| 6 | Try to attach `sample.txt` (click the icon or drag and drop the file into the chat) | File is not attached and an error message is displayed |

## Expected Final State

The chat attach capability follows the Attachments module switch.

## Pass/Fail Criteria

**Pass:**
- ON: file attaches and the Agent uses it; OFF: attach icon disabled and an error message is shown on attach attempt

**Fail:**
- Attach state does not follow the switch, a file attaches while OFF, or no error message is shown

## Notes

**Source functional tests:** ELITEA-4788
**Regression rationale:** Verifies that a module switched in the new dropdown actually changes runtime behaviour, not just the UI state. Agent-level coverage was a gap (only pipeline coverage exists in ELITEA-2066 / ELITEA-2059).
**Selected checkpoints:** Attach enabled and working when ON; disabled with error message when OFF.
