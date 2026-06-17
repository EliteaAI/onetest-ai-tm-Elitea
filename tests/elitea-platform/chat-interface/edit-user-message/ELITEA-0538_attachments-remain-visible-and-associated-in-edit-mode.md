---
id: ELITEA-0538
title: "Attachments remain visible and associated in edit mode"
priority: high
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0538: Attachments remain visible and associated in edit mode

**Module:** Edit User Message · **Priority:** High · **Type:** Functional

**Objective:** Verify attachments on the last user message are preserved during editing and after Cancel.

**Coverage:**
- Attachments visible in edit mode
- Attachments preserved after Cancel
- Attachment association maintained through Save and apply

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation where the last user message has an attached file (if attachments are supported in the context)

## Test Data

- Last user message with at least one file attachment (e.g., image or document)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a message with an attachment. Wait for the response. Click Edit on the last user message. | Edit mode opens. The attachment indicator/thumbnail remains visible alongside the editable text. |
| 2 | Click "Cancel". | Edit mode exits. Attachment is still shown with the original message in read-only view. |
| 3 | Click Edit again. Modify the text and click "Save and apply". | After regeneration completes, the attachment remains associated with the updated message (unless explicitly removed by the user). |

## Expected Final State

After regeneration completes, the attachment remains associated with the updated message (unless explicitly removed by the user).

## Pass/Fail Criteria

**Pass:**
- Attachment visible during edit mode
- Attachment preserved after Cancel
- Attachment still associated after Save and apply

**Fail:**
- Attachment disappears when entering edit mode
- Attachment lost after Cancel or Save and apply
- Attachment indicator breaks or errors
