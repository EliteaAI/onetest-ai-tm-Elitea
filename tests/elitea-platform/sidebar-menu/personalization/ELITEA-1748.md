---
id: ELITEA-1748
title: "Verify tools and agent capabilities work with Bare personality"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, tools, agents]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1748: Verify tools and agent capabilities work with Bare personality

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that tools and agent capabilities function correctly with Bare personality

## Preconditions

- User is logged into EliteA platform
- User has access to agents and tools (e.g., web search, calculator, file operations)
- User can create new conversations
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: "Provide step-by-step reasoning"
- Test prompts requiring tool usage:
  - "Search the web for latest AI news"
  - "Calculate 15% of 2,450"
  - "Create a Python function to reverse a string"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation with agent/tools enabled | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Enter custom instructions: "Provide step-by-step reasoning" | Instructions appear in field |
| 5 | Apply changes and close modal | Changes saved |
| 6 | Send message: "Search the web for latest AI news" | Agent uses web search tool, returns results |
| 7 | Verify tool usage indicator | Tool usage shown in UI (e.g., "Using web search...") |
| 8 | Verify response follows custom instructions | Response includes step-by-step reasoning |
| 9 | Send message: "Calculate 15% of 2,450" | Agent uses calculator tool, returns 367.5 |
| 10 | Verify calculation accuracy | Result is correct |
| 11 | Send message: "Create a Python function to reverse a string" | Agent generates code using appropriate tool |
| 12 | Verify code quality | Code is functional and follows custom instructions |
| 13 | Verify no personality traits in responses | Responses are neutral, only custom instructions applied |

## Expected Final State

- Tools and agents work correctly with Bare personality
- Custom instructions applied to tool-assisted responses
- Tool usage indicators display properly
- Responses maintain neutrality while following custom instructions
- No personality traits interfere with tool usage or results

## Pass/Fail Criteria

**Pass:**
- All tools function correctly with Bare personality
- Custom instructions followed in tool-assisted responses
- Tool usage indicators work properly
- Results are accurate and well-formatted
- No personality traits appear in responses
- No errors or tool failures

**Fail:**
- Tools fail or malfunction with Bare personality
- Custom instructions ignored in tool-assisted responses
- Tool usage indicators broken or missing
- Results inaccurate or poorly formatted
- Personality traits leak into responses
- Errors or exceptions during tool usage
