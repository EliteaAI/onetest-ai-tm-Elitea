---
id: ELITEA-1304
title: "TTS Content Filtering — Lists, Headings, and Emoji Read Correctly [Parametrized: Numbered List | Bullet List | Headings | Emoji]"
priority: high
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [content-filtering, feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1304: TTS Content Filtering — Lists, Headings, and Emoji Read Correctly [Parametrized: Numbered List | Bullet List | Headings | Emoji]

**Module:** Text To Speech Tts · **Priority:** High · **Type:** Functional

**Objective:** Verify that TTS correctly reads lists, headings, and emoji with appropriate formatting and pausing — these are read rather than skipped, but formatting characters are filtered.

**Parameters:**
| # | Content type | Expected TTS behavior |
|---|---|---|
| 1 | Numbered list (≤5 items) | Read in order with natural pauses: "First... Second... Third..." |
| 2 | Bullet point list | Read with appropriate pauses between items; bullet symbols not spoken |
| 3 | Headings (H1/H2/H3) | Heading text read normally; `#` characters NOT spoken |
| 4 | Decorative emoji | Skipped in spoken output; functional emoji (✓, ✗) replaced with "yes"/"no" |

**Coverage:** All four content types are handled per the expected behavior above.

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each parameter: ask the LLM to produce a response containing the target content type (e.g., 'Give me a numbered list of 3 tips', 'List 3 bullet points', 'Write a response with H2 headings', 'Use checkmarks ✓ and ✗ in your response') | AI response contains the target content type |
| 2 | Click the TTS read-out button on the response | Audio playback starts |
| 3 | Listen to the audio for the section containing the target content type | Content is read as per the parameter table: lists with pauses, headings without #, emoji handled correctly |
| 4 | Repeat for all 4 parameter variants | All 4 content types are handled correctly in TTS output |

## Expected Final State

All 4 content types are handled correctly in TTS output

## Pass/Fail Criteria

**Pass:**
- Lists are read with natural pauses; bullet/number symbols not spoken verbatim
- Headings read without `#` characters
- Decorative emoji skipped; functional emoji labeled correctly

**Fail:**
- `#` characters spoken in headings
- Bullet symbols or numbers read as plain characters without natural pausing
- Functional emoji not labeled or decorative emoji read as unicode
