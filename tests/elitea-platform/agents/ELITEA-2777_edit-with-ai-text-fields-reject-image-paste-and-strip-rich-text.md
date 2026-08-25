---
id: ELITEA-2777
title: "Edit with AI wizard text fields reject image paste and strip rich-text formatting on paste"
priority: high
type: bug
module: agents
status: draft
execution_type: manual
tags: [feat:agents, bug-env:dev, bug-area:current-release-scope, r-2.0.5]
requirements: [EliteaAI/elitea_issues#6040]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent's configuration page is open
- An image file is available on the clipboard (copied from an image editor, browser, or file explorer)
- Rich-text content is available on the clipboard (e.g. bold/colored text copied from a Word document or formatted webpage)

## Test Data

| Field | Value |
|-------|-------|
| Clipboard content #1 | An image (e.g. PNG copied from an image viewer) |
| Clipboard content #2 | Rich-text content with formatting (bold, color, font size) copied from a document/webpage |
| Target text fields | Suggested Name, Suggested Description, Suggested Instructions, Suggested Welcome Message, Suggested Chat Starters (General / Instructions / User Interaction steps) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI with a general prompt | Prompt accepted |
| 2 | Generate the draft and navigate to the General step | Suggested Name and Description text fields are shown, editable |
| 3 | Copy an image to the clipboard and paste it into the Suggested Name field | The image is rejected — no image is inserted or embedded; field either rejects the paste or inserts nothing |
| 4 | Repeat the image paste into the Suggested Description field | The image is rejected in the same way |
| 5 | Copy rich-text content (with bold/color/font formatting) to the clipboard and paste it into the Suggested Description field | Only plain text content is inserted; all rich-text formatting (bold, color, font size) is stripped |
| 6 | Navigate to the Instructions step and repeat the image paste into the Suggested Instructions field | The image is rejected — no image is inserted or embedded |
| 7 | Repeat the rich-text paste into the Suggested Instructions field | Only plain text is inserted; formatting is stripped |
| 8 | Navigate to the User Interaction step and repeat both the image paste and rich-text paste into the Suggested Welcome Message and Suggested Chat Starters fields | Image pastes are rejected; rich-text pastes are reduced to plain text in both fields |
| 9 | Complete the wizard and apply changes | Modal closes without error |
| 10 | Verify the applied Agent fields | No embedded images or rich-text markup/styling are present in any field; only plain text content is saved |

## Expected Final State

All Edit with AI wizard text fields behave like plain-text inputs: image paste is rejected without inserting any image data, and pasted rich-text content is reduced to plain text with no residual formatting, matching the behavior of the standard (non-AI) agent edit form.

## Pass/Fail Criteria

**Pass:**
- No image can be pasted/embedded into any Suggested text field
- Rich-text formatting is stripped on paste, leaving only plain text, in every affected field

**Fail:**
- An image is successfully pasted/embedded into any Suggested text field
- Rich-text formatting (bold, color, font size, etc.) is preserved after pasting into any Suggested text field
