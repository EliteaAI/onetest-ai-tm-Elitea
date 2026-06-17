---
id: ELITEA-0903
title: "Send Button Behavior With File Attached but No Text"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0903: Send Button Behavior With File Attached but No Text

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify the Send button behavior when a file is attached but the text input is empty in the pipeline chat — behavior should be consistent with agent/chat behavior.

**Coverage:**
- File attached, text input empty
- Send button state (enabled or blocked)
- If blocked: a clear indication shown to the user

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

- File: image.png
- Text input: empty

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Click the paperclip and select image.png. | File thumbnail appears in input. Text input remains empty. |
| 2 | Observe the Send button state. | Send button is disabled — consistent with requiring text |

## Expected Final State

Send button is disabled — consistent with requiring text

## Pass/Fail Criteria

**Pass:**
- Send button behavior is consistent and clearly communicated
- No silent failure or unhandled error regardless of button state

**Fail:**
- Send button enabled but pipeline run errors silently
- Send button disabled with no explanation
