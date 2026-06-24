---
id: ELITEA-0010
title: "Test Bare personality with custom JSON formatting instructions"
priority: critical
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, json-output, custom-instructions]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-0010: Test Bare personality with custom JSON formatting instructions

**Module:** Chat · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Bare personality respects custom instructions for JSON formatting

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Bare personality is available in personality dropdown

## Test Data

- Custom instructions: "Always respond in valid JSON format. Use keys: 'answer', 'confidence', 'sources'."
- Test messages:
  - "What is Python?"
  - "Explain Docker containers"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens successfully |
| 3 | Select "Bare" personality | Bare personality selected |
| 4 | Enter custom instructions: "Always respond in valid JSON format. Use keys: 'answer', 'confidence', 'sources'." | Instructions appear in field |
| 5 | Apply changes and close modal | Changes saved |
| 6 | Send message: "What is Python?" | Response is valid JSON with keys: answer, confidence, sources |
| 7 | Copy response and validate JSON syntax | JSON parses without errors |
| 8 | Verify JSON structure | Contains all three required keys with appropriate values |
| 9 | Send message: "Explain Docker containers" | Response is valid JSON with same structure |
| 10 | Validate second response JSON | JSON parses correctly with required keys |
| 11 | Verify no prose outside JSON | Response contains only JSON, no explanatory text |

## Expected Final State

- All responses are valid JSON
- JSON structure matches custom instructions (answer, confidence, sources keys)
- No prose or explanatory text outside JSON format
- JSON is properly formatted and parseable
- Custom instructions respected consistently

## Pass/Fail Criteria

**Pass:**
- All responses are valid, parseable JSON
- Required keys (answer, confidence, sources) present in all responses
- No text outside JSON structure
- JSON formatting is clean and readable
- Custom instructions followed consistently

**Fail:**
- Any response is not valid JSON
- Missing required keys in JSON structure
- Prose or text appears outside JSON
- JSON parsing errors
- Custom instructions ignored or partially followed
