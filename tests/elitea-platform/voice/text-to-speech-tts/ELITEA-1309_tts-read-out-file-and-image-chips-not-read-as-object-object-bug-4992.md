---
id: ELITEA-1309
title: "TTS Read Out — File and Image Chips Not Read as \"Object object\" [Bug #4992]"
priority: critical
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4992, EliteaAI/elitea_issues#4500]
---
# ELITEA-1309: TTS Read Out — File and Image Chips Not Read as "Object object" [Bug #4992]

**Module:** Text To Speech Tts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the TTS "Read out" button does not read file or image chips as "Object object". Chips should either be skipped silently or replaced with a neutral phrase like "Attachment included".

**Bug Reference:** #4992 — TTS reads generated file/image chips as "Object object" (one occurrence per chip) when the user manually clicks "Read out".

**Important note:** This bug is reproducible ONLY when the user manually clicks the "Read out" button on the response. In Speaking Mode (auto-read after generation), "Object object" is NOT heard — this is an existing known distinction.

**Coverage:**
- Generated text file chip (.txt) → not read as "Object object"
- Generated markdown file chip (.md) → not read as "Object object"
- Generated SVG chip → not read as "Object object"
- Generated PNG image chip → not read as "Object object"
- Chip is either skipped silently or announced neutrally

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- An agent or pipeline capable of generating file/image output is available (e.g., artifact creation or image generation)
- Speaking Mode is OFF (test covers manual "Read out" only)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Request the LLM/agent to generate a file output (e.g., 'Create a copy of an image from bucket as PNG' or 'Generate a .txt summary file'). Wait for the response with the file/image chip. | AI response includes one or more file or image chips appended at the end |
| 2 | Ensure Speaking Mode is OFF. Click the TTS 'Read out' button on the response manually. | TTS audio playback starts |
| 3 | Listen carefully at the end of the response where the chip(s) appear | No 'Object object' is spoken. The chip is either silently skipped or announced with a neutral phrase (e.g., 'Attachment included'). |
| 4 | Repeat for each chip type: .txt, .md, .svg, .png (generate responses that produce each chip type) | All chip types pass — none produce 'Object object' in spoken output |

## Expected Final State

All chip types pass — none produce 'Object object' in spoken output

## Pass/Fail Criteria

**Pass:**
- No "Object object" is spoken for any chip type
- Chip is either silently skipped or announced as "Attachment included" or similar

**Fail:**
- TTS speaks "Object object" for any file or image chip when "Read out" is clicked manually
