---
id: ELITEA-2059
title: "Pipeline — Attach Files in Chat"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_attach_files_in_chat.test_attach_files_in_chat
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2439
---

# ELITEA-2059: Pipeline — Attach Files in Chat

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that files can be attached in the chat panel of a pipeline with the Attachments module enabled, and that the pipeline actually resolves the attached file's content (not merely acknowledges that a file was attached).

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with the Attachments module enabled is open.
- **An Artifact toolkit (pointed at the project's `attachments` bucket) is attached to the pipeline's Tools section AND selected in the LLM node's Toolkits field, with the node's Task mapping and pipeline state configured so the attachment's content is actually reachable.** Without this, the LLM has no mechanism to read the attachment's bytes — it only sees a path-like reference in the message text and can only honestly report that it cannot access the content. (Added 2026-10-15 — see Revision History; this configuration is what step 7's expected result below depends on.)

---

## Test Data

| Field | Value |
|-------|-------|
| File type | .txt or .png |
| File content | Literal, unambiguous content a human/LLM can verify by reading it (e.g. a file containing only the word "cat") — not merely a token matched by filename or a generic keyword. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline that has an Artifact toolkit attached to its Tools section and selected in the LLM node's Toolkits field (Attachments module enabled in Tools) | Pipeline is open with attachments-enabled chat panel; the attached toolkit is visible in the Tools section |
| 2 | In chat panel, locate "Attach Files (10 left)" button | Attach files button is visible and enabled |
| 3 | Click the attach files button | File picker opens |
| 4 | Upload a supported file with literal, unambiguous content (e.g., a .txt file containing only the word "cat") | File is uploaded and appears as attachment |
| 5 | Verify file appears as attachment in the message area | Attachment thumbnail or name is shown in the message area |
| 6 | Send a message that requires resolving the attachment's actual content (e.g. "What animal is in the attachment?") — not a generic "summarize the file" request | Message with attachment is sent |
| 7 | Verify pipeline processes the attachment | Pipeline responds with the correct fact extracted from the attached file's actual content (e.g. correctly names the animal described in the file) — not merely an acknowledgment that a file was attached |

---

## Expected Final State

A file is successfully attached in the chat, included in the sent message, and the pipeline's response correctly reflects the attached file's actual content.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File is attached, shown in message area, sent, and the pipeline's response correctly reflects the file's actual content.

**Fail:**
- Any step produces an error or unexpected result.
- File cannot be attached, is not shown, or the pipeline's response does not correctly reflect the attached file's content (including a response that only acknowledges the attachment without resolving it).

---

## Revision History

- **2026-10-15** — Corrected per issue [EliteaAI/elitea-testing-public#2408](https://github.com/EliteaAI/elitea-testing-public/issues/2408), overturning the earlier triage on parked question [#2412](https://github.com/EliteaAI/elitea-testing-public/issues/2412). The case previously described a bare LLM node and accepted a generic "I can't access the contents" acknowledgment as a pass — that was behavior drift, not the case's real intent. Added the Artifact-toolkit precondition (step 1) and strengthened step 7's expected result from "acknowledges or references the attachment" to "correctly resolves the attachment's actual content." See the automation's AFS (`test-specs/pipelines/l2_pipeline-attach-files-in-chat_ELITEA-2059.md` in `elitea-testing-public`) for full detail and live-verification evidence.
