---
id: ELITEA-1284
title: "Speaking Mode — TTS Content Filtering Applied During Auto-Read"
priority: medium
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [content-filtering, feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1284: Speaking Mode — TTS Content Filtering Applied During Auto-Read

**Module:** Speaking Mode · **Priority:** Medium · **Type:** Functional

**Objective:** Verify TTS content filtering rules are applied during Speaking Mode auto-read: code blocks announced neutrally, URLs simplified, and markdown syntax not spoken aloud.

**Coverage:** Code block → neutral announcement; URL → simplified phrase; markdown symbols (**, #, -) → not spoken.

## Preconditions

- Speaking Mode active on Chat page; speakers/headphones functional

## Test Data

Request: "Write a Python function to add two numbers, include https://python.org as reference, use bold headers and bullet points"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Speak: "Write a Python function to add two numbers, include https://python.org as a reference, use bold headers and bullet points". Let auto-send fire. | AI responds with code block, URL, and markdown formatting |
| 2 | TTS auto-reads the response. Listen at the code block section. | Code block is announced neutrally (e.g., "code block"), not read character-by-character |
| 3 | Listen at the URL section. | URL simplified to a phrase (e.g., "a link" or "the python.org link"), not spoken verbatim |
| 4 | Listen through markdown-formatted sections (bold headers, bullet points). | Markdown symbols (**, #, -) are not spoken; text content read naturally |

## Expected Final State

Markdown symbols (**, #, -) are not spoken; text content read naturally

## Pass/Fail Criteria

**Pass:**
- Code block announced neutrally (not read character-by-character); URL simplified (e.g., "the link"); markdown symbols (**, #, -) not spoken

**Fail:**
- Code read verbatim character-by-character; full URL spoken; markdown symbols spoken aloud
