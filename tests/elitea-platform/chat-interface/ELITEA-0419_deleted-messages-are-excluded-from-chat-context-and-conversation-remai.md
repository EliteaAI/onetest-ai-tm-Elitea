---
id: ELITEA-0419
title: "Deleted Messages Are Excluded From Chat Context and Conversation Remains Functional [Parametrized: Chat / Agent / Pipeline]"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [rca:integration-issue, nfr:usability, eng:frontend, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3954]
---
# ELITEA-0419: Deleted Messages Are Excluded From Chat Context and Conversation Remains Functional [Parametrized: Chat / Agent / Pipeline]

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that deleted message pairs are excluded from the AI's context in subsequent requests, and that the conversation — including a fully emptied one — remains functional after all messages are deleted, across Chat, Agent, and Pipeline pages.

**Coverage:**
- Deleted exchanges are not referenced by the AI in subsequent responses
- Conversation remains interactive after partial and full deletion of message pairs
- Empty conversation state (all exchanges deleted) accepts new messages without error
- Behavior is consistent across Direct Chat, Agent Chat, and Pipeline Chat

## Preconditions

- Logged into ELITEA as a standard user at {{base_url}}
- Conversations with ≥3 user input/response pairs available on each of: Chat page, Agent chat page, Pipeline chat page
- Browser: Chrome (latest)

## Test Data

- Conversation with 3 exchanges: A1/R1 (e.g. "What is the capital of France?"), A2/R2 (e.g. "What is 2+2?"), A3/R3 (e.g. "Tell me a joke")
- Exchange to delete: A2/R2
- Follow-up message: "Summarize everything we discussed so far"
- Post-empty message: "Hello, can you help me?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Direct Chat conversation with at least 3 exchanges (A1/R1, A2/R2, A3/R3). | All 3 exchanges are visible. |
| 2 | Delete exchange A2/R2 (response first, then the paired user input if not auto-removed). | Both messages of the A2/R2 exchange are removed. A1/R1 and A3/R3 remain intact. |
| 3 | Send a follow-up message: 'Summarize everything we discussed so far'. | AI response summarizes only A1/R1 and A3/R3 content. No reference to the deleted A2/R2 exchange. |
| 4 | Delete all remaining exchanges until the conversation is empty. | All messages are removed. Conversation displays in a clean empty state with no errors. |
| 5 | Send a new message in the now-empty conversation. | New message sends successfully. A response is received. Conversation is fully functional. |
| 6 | Repeat steps 1–5 for Agent Chat. | Same behavior: deleted content excluded from context, conversation functional after full deletion. |
| 7 | Repeat steps 1–5 for Pipeline Chat. | Same behavior: deleted content excluded from context, conversation functional after full deletion. |

## Expected Final State

Same behavior: deleted content excluded from context, conversation functional after full deletion.

## Pass/Fail Criteria

**Pass:**
- AI responses after deletion do not reference content from deleted exchanges
- Conversation remains interactive after partial and full deletion
- Empty conversation accepts new messages and returns responses without error
- Behavior is consistent across Direct Chat, Agent Chat, and Pipeline Chat

**Fail:**
- AI references content from deleted exchanges in subsequent responses in any context
- Conversation enters a broken or non-interactive state after deletion
- Empty conversation cannot accept new messages or shows an error
- Behavior is inconsistent across the three contexts
