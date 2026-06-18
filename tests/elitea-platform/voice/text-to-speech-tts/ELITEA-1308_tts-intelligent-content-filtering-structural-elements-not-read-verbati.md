---
id: ELITEA-1308
title: "TTS Intelligent Content Filtering — Structural Elements Not Read Verbatim [Parametrized: Code Block | Inline Code | Markdown Markers | Table | JSON/XML/YAML | URL | File Path]"
priority: critical
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [content-filtering, feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1308: TTS Intelligent Content Filtering — Structural Elements Not Read Verbatim [Parametrized: Code Block | Inline Code | Markdown Markers | Table | JSON/XML/YAML | URL | File Path]

**Module:** Text To Speech Tts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that TTS intelligent content filtering correctly handles structural markdown/code elements — none of these are read verbatim; each is either skipped or replaced with a neutral announcement.

**Parameters:**
| # | Content type | Expected TTS output |
|---|---|---|
| 1 | Multi-line code block (` ``` ... ``` `) | "A code example has been included. Please review it on screen." |
| 2 | Inline code (single backtick) | Spoken without backtick characters — only content or a label |
| 3 | Markdown formatting markers (`**`, `_`, `#`, `-`) | NOT read aloud as characters |
| 4 | Markdown table | "A table has been included. Please review it on screen." |
| 5 | JSON / XML / YAML code block | "Structured data has been included. Please review it on screen." |
| 6 | URL in response | Replaced with "the link" — full URL not spoken |

**Coverage:** All seven structural element types are filtered correctly; natural language text around them is read normally.

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each parameter: ask the LLM to produce a response containing the target content type (e.g., 'Show me a Python code block', 'Give me a summary table', 'List some URLs', etc.) | AI response contains the requested content type alongside natural language text |
| 2 | Click the TTS read-out button on the response | Audio playback starts |
| 3 | Listen to the audio at the section containing the target content type | The content type is handled as specified in the parameter table. The surrounding natural language text is read normally. |
| 4 | Repeat steps 1–3 for each of the 6 parameter variants | All 7 content types are filtered correctly in TTS output |

## Expected Final State

All 7 content types are filtered correctly in TTS output

## Pass/Fail Criteria

**Pass:**
- Each content type is filtered/announced as specified in the parameter table
- Surrounding natural language text is read normally

**Fail:**
- Any content type is read verbatim (e.g., backtick characters spoken, full URL read out, JSON content read character by character)
- Natural language text is suppressed or garbled
