# Test Cases for "Bare" Personality Feature

**Feature Issue:** [#5264 - Add "Bare" Personality Type](https://github.com/EliteaAI/elitea_issues/issues/5264)  
**Related Sub-issue:** [#5394 - Personalization API returns legacy description field](https://github.com/EliteaAI/elitea_issues/issues/5394)  
**Target Release:** R-2.0.4  
**Test Case Count:** 6 (Initial batch - P0 Critical and P1 High Priority)

## Overview

This test suite validates the implementation of the "Bare" personality type feature, which provides users with a minimal LLM experience—no EliteA branding, only their custom instructions plus tool-required guidance.

## Feature Summary

The "Bare" personality type:
- Appears in User Settings → Personalization → Default Personality dropdown
- Appears in Context Management modal → User Instructions → Persona dropdown
- Bypasses all EliteA-injected prompt content
- With NO custom instructions → empty system message to LLM
- With custom instructions → ONLY those instructions sent (no wrapper)
- LLM responds with its native identity (Claude, ChatGPT, etc.)
- Context management, token tracking, and tools still function normally

## Test Cases Included

_IDs renumbered from ELITEA-1718–1723 to ELITEA-3790–3795 (see `CASE_ID_CHANGES.md`)._

### P0 - Critical Functionality (5 test cases)

1. **ELITEA-3790:** Verify "Bare" option appears in Context Management modal
2. **ELITEA-3791:** Verify "Bare" can be selected and saved in User Settings
3. **ELITEA-3792:** Verify empty system prompt with Bare mode (no custom instructions)
4. **ELITEA-3793:** Verify custom instructions only with Bare mode
5. **ELITEA-3794:** Verify LLM native identity in Bare mode

### P1 - High Priority (1 test case)

6. **ELITEA-3795:** Verify context management functions in Bare mode

## Test Coverage

### Components Affected
- **EliteaUI:** User Settings, Context Management modal, personality constants
- **elitea_core:** API endpoints, conversation persistence
- **elitea-sdk:** Assistant.getLangGraphReactAgent(), persona bypass logic

### Key Validation Areas
- ✅ UI visibility (dropdowns, options, descriptions)
- ✅ Selection and persistence (save, reload, session)
- ✅ System prompt behavior (empty, custom-only, no branding)
- ✅ LLM behavior (native identity, custom instruction following)
- ✅ Context management (summarization, token tracking)

## Execution Instructions

### Prerequisites
- Access to EliteaUI dev/staging environment
- Valid test user account with personalization access
- Browser with Developer Tools (Chrome/Firefox/Edge)
- Access to multiple LLM providers (Claude, ChatGPT) for identity tests
- SDK debug logging enabled (optional but helpful)

### Test Environment
- **Environment:** dev.elitea.ai or staging.elitea.ai
- **Browser:** Chrome (latest), Firefox (latest)
- **User Role:** Standard user with conversation access

### Execution Order
1. Run P0 test cases first (critical functionality)
2. Run P1 test cases (high priority features)
3. Document any failures with screenshots and logs
4. Report defects with appropriate severity

## Test Data

### Sample Custom Instructions
- Language test: `"Always respond in Spanish"`
- Format test: `"Always respond in JSON format"`
- Behavior test: `"You are a pirate. Always speak like a pirate."`
- Complex test: `"You are an expert in Python programming.\n\nWhen answering:\n1. Always provide code examples\n2. Explain each line of code\n3. Include error handling"`

### Expected Dropdown Options
- Bare
- Cynical
- Generic
- Nerdy
- None
- QA
- Quirky

## Known Issues & Dependencies

### Blocking Issues
- None currently

### Related Sub-Issues
- **#5394:** Ensure Personalization API does NOT return legacy description field for "bare" persona

### Dependencies
- Backend: "bare" value must be accepted in conversation.meta.persona
- SDK: persona == 'bare' must bypass all template injection
- UI: Constants must include "bare" with correct description

## Estimated Execution Time

- **P0 test cases:** ~2 hours
- **P1 test cases:** ~30 minutes
- **Total:** ~2.5 hours (manual execution)

## Automation Potential

The following test cases are good candidates for automation:
- ELITEA-3790, ELITEA-3791: UI visibility and selection (Playwright)
- ELITEA-3792, ELITEA-3793: System prompt validation (API mocking)

## Reporting

### Pass Criteria
- All P0 test cases must PASS
- At least 80% of P1 test cases must PASS

### Defect Severity Guidelines
- **Critical:** "Bare" option not visible or not selectable
- **High:** EliteA branding still appears in Bare mode
- **Medium:** Context management issues in Bare mode
- **Low:** Minor UI inconsistencies (spacing, alignment)

## Additional Test Cases

This initial batch covers the most critical functionality. Additional test cases for the following areas are documented separately:
- Regression testing (existing personalities: Generic, QA, Nerdy, Quirky, Cynical, None)
- Edge cases (very long instructions, special characters, multiline)
- Different LLM providers (OpenAI, Anthropic, Google)
- SDK integration and logging
- Performance and token limits

**Total comprehensive test suite:** 36 test cases (17 P0 + 19 P1)

## Contact

**QA Lead:** Mariam Hakobyan  
**Test Environment:** dev.elitea.ai  
**Documentation:** [CLAUDE.md](../../../.claude/CLAUDE.md)

---

**Last Updated:** 2026-06-25  
**Status:** Ready for execution
