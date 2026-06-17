---
id: ELITEA-0176
title: "Admin Can Review Published Agents List and Unpublish a Rule-Violating Agent With Reason"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3773, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3773]
---
# ELITEA-0176: Admin Can Review Published Agents List and Unpublish a Rule-Violating Agent With Reason

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a platform admin can view all published agents in the Admin section, select a rule-violating agent, provide an unpublish reason, and immediately remove it from Agents Studio — while preserving existing user conversations in a disabled state.

**Coverage:**
- Admin can see all published agents with full details
- Unpublish option available per agent in Admin section
- Admin must provide a reason before confirming unpublish
- Agent removed from Agents Studio immediately after admin unpublish
- Agent not searchable or discoverable after removal
- Existing conversations with the agent are preserved (history intact) but input is disabled

## Preconditions

- Logged in as Platform Admin on {{base_url}}
- Agent P (published by User A) is visible in Agents Studio
- User B has an existing open conversation with Agent P

## Test Data

- Agent P name: note exact name from environment
- Unpublish reason: "Agent violates platform content guidelines — contains inappropriate tool instructions"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Public Project → Agents → Admin section | Admin page loads with list of published agents |
| 2 | Locate Agent P in the published agents list | Agent P is visible with name, author (User A), publish date, and version |
| 3 | Click the Unpublish option next to Agent P | A confirmation dialog or form appears |
| 4 | Enter the reason: "Agent violates platform content guidelines — contains inappropriate tool instructions" | Reason is entered in the reason field |
| 5 | Confirm the unpublish action | Confirmation succeeds; success notification shown |
| 6 | Verify Agent P is removed from the Admin published agents list | Agent P no longer appears in the Admin list |
| 7 | Navigate to Agents Studio, search for Agent P by name | Agent P is NOT found in Studio search results |
| 8 | Browse all Studio categories | Agent P's card is not present in any category |
| 9 | As User B, open the existing conversation with Agent P | Conversation page loads (no crash); all prior messages are visible |
| 10 | Attempt to send a new message in User B's conversation | Input field is disabled; Send button is absent or disabled; message cannot be sent |

## Expected Final State

Input field is disabled; Send button is absent or disabled; message cannot be sent

## Pass/Fail Criteria

**Pass:**
- Admin unpublish with reason succeeds and returns a success notification
- Agent P is immediately removed from Agents Studio search and category browse
- User B's existing conversation history is intact and visible
- User B cannot send new messages in the disabled conversation

**Fail:**
- Agent P remains visible in Agents Studio after admin unpublish
- Admin can unpublish without providing a reason (reason field is optional or absent)
- User B's prior conversation history is lost or corrupted
- User B can still send new messages despite admin unpublish
