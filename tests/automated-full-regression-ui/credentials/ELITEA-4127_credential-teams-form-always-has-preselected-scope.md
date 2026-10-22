---
id: ELITEA-4127
title: "Credential — Teams Form Always Has at Least One Pre-selected Scope"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: [EliteaAI/elitea_issues#6835]
---

# ELITEA-4127: Credential — Teams Form Always Has at Least One Pre-selected Scope

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Teams credential form shows the Scopes field as a list of checkboxes with the default read scopes pre-selected, and that the user can never untick the last selected scope.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Teams |
| Default (pre-selected) scopes | User.ReadBasic.All, Chat.Read, Team.ReadBasic.All, Channel.ReadBasic.All |
| Optional (not pre-selected) scopes | ChatMessage.Send, Chat.Create, ChannelMessage.Send |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}` → Credentials → click **+ Create** and select credential type "Teams" | Teams credential form opens with the **Default app** auth option |
| 2 | Locate the **Scopes** field | Scopes is shown as a list of 7 checkboxes, not a text input |
| 3 | Check the initial checkbox state | The 4 default scopes are ticked; ChatMessage.Send, Chat.Create and ChannelMessage.Send are unticked |
| 4 | Untick checkboxes one by one until only one scope stays ticked | Each untick is applied; the last ticked checkbox becomes disabled and cannot be unticked |
| 5 | Try to click the last ticked checkbox | It stays ticked; at least one scope is still selected |
| 6 | Switch the auth option to **Custom app** and check the Scopes field | Scopes checkbox list is shown with at least one scope ticked |

---

## Expected Final State

The Teams credential form never has zero scopes selected: the defaults are pre-selected on open, and the last ticked scope cannot be unticked.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- At least one scope checkbox is ticked at every point of the test.

**Fail:**
- The Scopes field opens with no checkbox ticked, or the default scopes differ from the Test Data.
- The user can untick all scope checkboxes.
