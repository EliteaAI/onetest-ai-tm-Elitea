---
id: ELITEA-4788
title: "Attachments module switch in the Modules dropdown controls the chat attach icon and file attachment"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, attachments, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4788: Attachments module switch in the Modules dropdown controls the chat attach icon and file attachment

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the Attachments module is switched ON in the "+ Modules" dropdown, the attach icon in the Agent chat is enabled and files can be attached, and when it is switched OFF, the attach icon is disabled and an attempt to attach shows an error message.

**Coverage:**
- Attachments ON: attach icon enabled, file attached successfully
- Attachments OFF: attach icon disabled, error message on attach attempt

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists
- Attachments module is available on the environment
- Browser: Chrome (latest)

## Test Data

A small text file (e.g. `sample.txt`, < 1 KB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent, click "+ Modules" and switch Attachments ON | Attachments switch shows ON |
| 2 | Click Save | Agent is saved |
| 3 | Open the Agent chat panel | Attach icon is displayed and enabled |
| 4 | Click the attach icon and select `sample.txt` | File is attached and shown in the chat input |
| 5 | Send a message asking the Agent to summarize the file | Message is sent with the attachment and the Agent responds using the file content |
| 6 | Click "+ Modules", switch Attachments OFF and click Save | Agent is saved with Attachments OFF |
| 7 | Open the Agent chat panel | Attach icon is disabled |
| 8 | Try to attach `sample.txt` (click the disabled icon or drag and drop the file into the chat) | File is not attached and an error message is displayed explaining that attachments are not available |

## Expected Final State

The chat attach icon and file attachment follow the Attachments module switch.

## Pass/Fail Criteria

**Pass:** With Attachments ON, files can be attached; with Attachments OFF, the icon is disabled and an attach attempt shows an error message
**Fail:** Attach icon state does not follow the switch, files can be attached while OFF, or no error message is shown when attaching is not possible
