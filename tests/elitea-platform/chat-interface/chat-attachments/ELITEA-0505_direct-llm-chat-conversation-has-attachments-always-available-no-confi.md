---
id: ELITEA-0505
title: "Direct LLM chat conversation has attachments always available — no configuration required"
priority: high
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0505: Direct LLM chat conversation has attachments always available — no configuration required

**Module:** Chat Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a direct LLM chat conversation (no agent selected), the paperclip icon is enabled by default without requiring any agent configuration, artifact toolkit setup, or toggle — and that files are automatically stored in the default `attachments` bucket.

**Coverage:**
- Paperclip icon immediately active in direct LLM chat
- No configuration dialog or setup step required
- File browser opens on paperclip click
- File uploaded and stored in default `attachments` bucket without any toolkit configuration
- Behavior consistent across multiple LLM model types

## Preconditions

- Logged into ELITEA at {{base_url}}
- No artifact toolkit configured, no agent selected
- Any small file available locally (e.g., `test.png`, < 1 MB)

## Test Data

- Model: GPT-5.2 (or any direct LLM — no agent wrapper)
- File: `test.png` (~500 KB)
- Prompt: "Describe this image"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar → click New Conversation → select any LLM model directly (not an agent) | Chat input is visible with the paperclip icon |
| 2 | Inspect the paperclip icon without clicking anything | Paperclip is immediately active and enabled — no setup prompt, no configuration dialog, no toggle to activate |
| 3 | Click the paperclip icon | File browser opens immediately; no error or 'setup required' message |
| 4 | Select `test.png` → type "Describe this image" → Send | File attached and message sent successfully; AI returns image description |
| 5 | Navigate to Artifacts → check the `attachments` bucket | `test.png` appears in the default `attachments` bucket with no manual toolkit configuration |

## Expected Final State

`test.png` appears in the default `attachments` bucket with no manual toolkit configuration

## Pass/Fail Criteria

**Pass:**
- Paperclip active immediately in direct LLM chat — no setup required
- File browser opens on click
- File stored in default `attachments` bucket automatically

**Fail:**
- Paperclip disabled or requires configuration
- Error saying 'artifact toolkit not configured'
- File not found in `attachments` bucket
