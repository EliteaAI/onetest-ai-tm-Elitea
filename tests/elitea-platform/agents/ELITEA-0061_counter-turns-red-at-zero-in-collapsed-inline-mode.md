---
id: ELITEA-0061
title: "Counter Turns Red at Zero in Collapsed (Inline) Mode"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [meta:reported-by-support, nfr:validation, nfr:usability, eng:frontend, feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4963]
---
# ELITEA-0061: Counter Turns Red at Zero in Collapsed (Inline) Mode

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify the existing Collapsed mode counter changes to red and the warning message appears when the character count reaches 0 for Welcome Message and Conversation Starter fields.

**Coverage:**
- Counter color turns red at BV1 (768 chars) in Collapsed mode
- Warning "0 characters left. You have reached the MAXIMUM character limit" shown at limit
- Input blocked or truncated at BV2 (769 chars)
- Counter reverts to default color above 0

## Preconditions

- Logged in to {{base_url}}
- Existing agent open in edit mode
- Full Screen editor is NOT open — fields are in Collapsed (standard inline) mode

## Test Data

- BV1: 768-character string — exactly at the character limit (counter = 0)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click into the Welcome Message field in the left configuration panel (Collapsed mode). Type 1 character. | Character counter is visible in default (non-red) color. |
| 2 | Clear the field. Paste the BV1 string (768 chars). | Counter color changes to red. Warning message '0 characters left. You have reached the MAXIMUM character limit' is displayed. |
| 3 | Delete 1 character. | Counter shows '0 characters left'. Counter color reverts to default. Warning message disappears. |
| 4 | Click into a Conversation Starter entry (Collapsed mode). Repeat steps 1–3 for this field. | Same counter color and warning message behavior observed for Conversation Starters in Collapsed mode. |

## Expected Final State

Same counter color and warning message behavior observed for Conversation Starters in Collapsed mode.

## Pass/Fail Criteria

**Pass:**
- Counter turns red at exactly 0 (BV1) in Collapsed mode for both fields
- Warning "0 characters left. You have reached the MAXIMUM character limit" appears at 0
- Counter and warning revert to default when count rises above 0

**Fail:**
- Counter does not change color at 0 in Collapsed mode for either field
- Warning message is missing or shows different text
- Counter turns red at wrong threshold
