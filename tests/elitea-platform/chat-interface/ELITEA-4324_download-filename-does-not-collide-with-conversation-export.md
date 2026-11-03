---
id: ELITEA-4324
title: "Downloaded Code Block Filename Does Not Conflict With or Mimic Conversation Export Naming"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- A chat conversation exists that contains at least one AI response with a code block, and the conversation can also be exported via the existing Conversation Export feature (reference: ELITEA-3762-3765 export-conversation suite)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Give me a short json config example" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat`, open a conversation, and send the Test Data prompt | AI responds with a json code block and a Download icon in its toolbar |
| 2 | Click the Download icon on the code block and note the downloaded filename and extension | File downloads with a filename/extension pattern specific to the code block (e.g. reflecting language/content, such as `code.json` or similar), distinct from a conversation-level export name |
| 3 | Trigger the existing Conversation Export feature on the same conversation (re-validation touchpoint vs ELITEA-3762-3765) | Conversation exports successfully with its own established filename/extension pattern (e.g. reflecting the conversation name/date, as `.json`/`.zip` per existing behavior) |
| 4 | Compare the two downloaded files' filenames | The code-block download filename and the conversation export filename are clearly distinguishable (do not share an identical name, do not overwrite one another in the same downloads folder, and do not visually suggest they are the same artifact) |
| 5 | Confirm both files exist independently in the downloads folder without one overwriting the other | Both files are present and intact |

## Expected Final State

The chat code-block Download filename pattern and the Conversation Export filename pattern remain clearly distinct, with no naming collision, overwrite, or user-facing confusion between the two features.

## Pass/Fail Criteria

**Pass:**
- Code-block download filename is distinct from the conversation export filename
- Neither download overwrites the other in the downloads folder
- No regression is observed in the existing Conversation Export naming behavior (ELITEA-3762-3765)

**Fail:**
- The two filenames are identical or easily confused
- One download overwrites or is overwritten by the other
- Conversation Export naming behavior has regressed
