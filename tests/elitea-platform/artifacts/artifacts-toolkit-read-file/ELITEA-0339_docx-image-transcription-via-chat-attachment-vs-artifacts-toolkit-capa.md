---
id: ELITEA-0339
title: "DOCX Image Transcription via Chat Attachment vs Artifacts Toolkit — Capability Boundary"
priority: medium
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4629]
---
# ELITEA-0339: DOCX Image Transcription via Chat Attachment vs Artifacts Toolkit — Capability Boundary

**Module:** Artifacts Toolkit Read File · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that DOCX embedded image transcription works via both the Chat Attachment path and the Artifacts Toolkit path, and confirm the capability difference between them.

**Coverage:**
- Chat Attachment path: `is_capture_image=True` transcribes all embedded images; `get_file_metadata` and `extra_params` are NOT available (no selective extraction)
- Artifacts Toolkit path: `is_capture_image=True` transcribes all embedded images; `get_file_metadata` IS available; `extra_params` enables selective extraction
- Both paths successfully produce image transcriptions
- Feature boundary confirmed: selective extraction is only possible via the Artifacts Toolkit path

## Preconditions

- Logged in to dev environment
- Multimodal LLM configured (Supports Vision = enabled)
- `docx_with_images.docx` (2 embedded images: image1.jpeg, image2.png) available locally and also uploaded to artifact bucket `test`
- Chat session with Allow Attachments enabled (for attachment path)
- Separate chat session with Artifact Toolkit configured for bucket `test` (for toolkit path)

## Test Data

| Path | File | Bucket | Tools available |
|---|---|---|---|
| Chat Attachment | docx_with_images.docx | attachments (auto) | readFile + is_capture_image=True only |
| Artifacts Toolkit | docx_with_images.docx | test | readFile + is_capture_image=True + get_file_metadata + extra_params |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | **[Attachment path]** In a chat session with Allow Attachments enabled, attach `docx_with_images.docx` via the paperclip icon and send: "Transcribe all embedded images in this document. Use is_capture_image=True." | File uploads. `readFile` is called with `is_capture_image=True`. Image transcriptions for all embedded images are returned. |
| 2 | **[Attachment path]** Attempt to call `get_file_metadata` on the attached file in the same session. | `get_file_metadata` is not available — it does not appear in the tool list. Selective extraction via `extra_params` is not possible on this path. |
| 3 | **[Attachment path]** Verify no `extra_params` can be passed in this context. | No `extra_params` support. All embedded images are transcribed when `is_capture_image=True` — no selective extraction possible. |
| 4 | **[Artifacts Toolkit path]** In a chat session with Artifact Toolkit configured for bucket `test`, call `get_file_metadata` on `docx_with_images.docx`. | Metadata returned: `image_count=2`, `image_names=["image1.jpeg", "image2.png"]`, `instruction_for_readFile` block present including `extra_params` guidance. |
| 5 | **[Artifacts Toolkit path]** Call `readFile` on `docx_with_images.docx` with `is_capture_image=True` and `extra_params` = `{"extracted_images_names": ["image1.jpeg"], "read_images_only": true}` as a JSON string. | Only `image1.jpeg` is transcribed. Document text suppressed. Selective extraction confirmed. |
| 6 | Compare the two paths: attachment path (all images, no selective control) vs artifacts toolkit path (selective extraction via `get_file_metadata` + `extra_params`). | Both paths produce image transcriptions. Attachment path: all images transcribed, no selective control. Toolkit path: selective extraction possible via `get_file_metadata` + `extra_params`. |

## Expected Final State

Both paths produce image transcriptions. Attachment path: all images transcribed, no selective control. Toolkit path: selective extraction possible via `get_file_metadata` + `extra_params`.

## Pass/Fail Criteria

**Pass:**
- Chat Attachment path: image transcription returned with `is_capture_image=True`
- Chat Attachment path: `get_file_metadata` not available; `extra_params` not applicable
- Artifacts Toolkit path: image transcription returned with `is_capture_image=True`
- Artifacts Toolkit path: `get_file_metadata` available and returns correct metadata; `extra_params` enables selective extraction

**Fail:**
- Either path fails to transcribe images when `is_capture_image=True` is set
- `extra_params` becomes available on the Chat Attachment path (unexpected scope creep)
- `get_file_metadata` unavailable on the Artifacts Toolkit path
