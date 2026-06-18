---
id: ELITEA-0525
title: "Toolkit Tool Calls Do Not Inflate Message Count or Token Count in Context [Parametrized]"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, feat:agents, issue:4471, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4471]
---
# ELITEA-0525: Toolkit Tool Calls Do Not Inflate Message Count or Token Count in Context [Parametrized]

**Module:** Context Management · **Priority:** High · **Type:** Functional

## Preconditions

- Logged in to {{base_url}}
- At least one configured toolkit (e.g. Artifacts) is added as a participant in a Chat or Agent conversation
- For Row 3: two different toolkits are added as participants (e.g. Artifacts + any other toolkit)
- In-context budget widget is visible

## Test Data

| # | Scenario | Request to send |
|---|---|---|
| 1 | 1 tool call — single toolkit | "List the files in my bucket." |
| 2 | 3–5 tool calls — single toolkit | "Create 3 files named a.txt, b.txt, c.txt in my bucket." |
| 3 | Multiple tool calls across 2 different toolkits | "List the files in my bucket and [do something with the second toolkit]." |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set up the conversation per the current test data row (add the required toolkit(s) as participants). Open the conversation. | Conversation is ready. In-context budget shows initial message count (N) and token count (T). |
| 2 | Send the request defined in the current row. Wait for the run to fully complete. | All tool chipsets complete. The assistant returns a final response. |
| 3 | Check the in-context budget message count. Calculate delta: new count − N. | Message delta = exactly +2 (1 user input + 1 assistant response). No extra messages from individual tool calls. |
| 4 | Check the in-context budget token count. Calculate delta: new token count − T. Verify: delta ≈ (tokens in your user message) + (tokens in the assistant’s final response). There should be no additional token overhead from intermediate tool call/result pairs. | Token delta matches user input + assistant response only. No unexplained extra tokens from tool invocations. |
| 5 | Send one simple follow-up message (e.g. "ok") and wait for the response. | The conversation continues normally. Message count and token count both increase further — they do NOT drop below the values recorded after Step 2. |
| 6 | Repeat Steps 1–5 for each remaining row in the test data table. | All rows pass Steps 3, 4, and 5. |

## Expected Final State

All rows pass Steps 3, 4, and 5.

## Pass/Fail Criteria

**Pass:**
- Message delta = +2 after each request, regardless of tool call count
- Token delta reflects only user input + assistant response — no hidden extra tokens from tool calls
- After a follow-up message, the total message count and token count are higher than before (context is preserved, not reset)

**Fail:**
- Message count grows by more than +2 per request
- Token count contains unexplained extra tokens beyond user input + response
- After a follow-up message, message or token count drops below the previously recorded value
