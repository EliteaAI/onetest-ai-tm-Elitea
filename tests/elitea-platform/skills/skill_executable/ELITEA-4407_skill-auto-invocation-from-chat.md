---
id: ELITEA-4407
title: "Skill Auto-Invocation from Chat Based on User Intent Without Explicit Participant"
priority: critical
type: functional
module: chat-skills-integration
status: ready
execution_type: manual
tags: [feat:chat, feat:skills, ui, skill-invocation, auto-invocation, metadata-matching]
requirements: [EliteaAI/elitea_issues#7126]
---
# ELITEA-4407: Skill Auto-Invocation from Chat Based on User Intent Without Explicit Participant

**Module:** Chat Skills Integration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the EliteA chat system can automatically invoke skills from the project's available skills based on user intent and skill metadata matching, even when the skill is NOT explicitly added as a chat participant, the user does NOT provide the exact skill name, and the system intelligently selects the appropriate skill based on metadata.

**Coverage:**
- Skill auto-invocation without being added as explicit participant
- Intelligent skill selection based on user intent and metadata matching
- Visual feedback (skill badge/icon) showing which skill was invoked
- Skill execution within chat context
- Participant list remains unchanged after auto-invocation
- Multiple consecutive auto-invocations work independently

## Preconditions

- User is logged into EliteA platform at {{base_url}}
- User has access to a project with at least one skill configured (e.g., "code-reviewer" skill)
- The skill has proper metadata configured (description, capabilities, tags) for intent matching
- User has appropriate permissions to use skills in the project
- Chat interface is accessible and functional
- The skill is **NOT** added as an explicit participant in the chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a project and open a new or existing chat | Chat interface loads successfully. Input field is active and ready. No skills are shown as explicit participants in the PARTICIPANTS panel. |
| 2 | In the chat input field, type a message that implies code review intent WITHOUT mentioning the skill name: "Review this code public class MyClass { private int value; }" | Text is entered successfully in the chat input field. No auto-complete or skill suggestions appear. |
| 3 | Press Enter or click the Send button to send the message | Message is sent and appears in chat history. System begins processing the request. Loading indicator appears (if applicable). |
| 4 | Observe the chat response area for visual feedback | A skill badge/icon appears showing which skill was auto-invoked (e.g., "Skill: code-reviewer"). Badge displays: skill icon (if configured), skill name or identifier, and clear visual indication that a skill is processing. Badge appears BEFORE or alongside the skill's response. User can clearly identify that a skill was invoked automatically. |
| 5 | Wait for the skill to complete processing | Skill executes successfully within the chat context. Response is relevant to the code review request. Response includes code analysis/feedback appropriate for the input (e.g., suggestions, issues, recommendations). No error messages appear. Response is formatted correctly (code blocks, highlights, markdown rendering). |
| 6 | Review which skill was invoked based on the badge/icon | The correct skill was selected based on user intent (e.g., "code-reviewer" for code review request). No inappropriate skill was invoked. System made intelligent decision based on metadata matching. |
| 7 | Check the chat PARTICIPANTS panel/list | The auto-invoked skill is NOT added as a permanent participant. Participant list remains unchanged from Step 1. Skill invocation is contextual and doesn't modify chat structure. |
| 8 | Send another message with DIFFERENT intent: "Can you help me debug this function?" | System processes the new request. May invoke a different skill appropriate for debugging (or same skill if metadata matches). Previous skill invocation doesn't interfere. Each message is evaluated independently for skill matching. |

## Expected Final State

- Chat remains in functional state
- Chat history contains all messages and skill responses with appropriate skill badges
- No skills are added as permanent participants
- No orphaned processes or hanging skill executions
- System is ready for the next user interaction

## Pass/Fail Criteria

**Pass:**
- Skill is automatically invoked without being an explicit participant
- Skill badge/icon appears clearly showing which skill was invoked
- Skill executes successfully and provides relevant response to user intent
- Correct skill is selected based on metadata and user intent
- Participant list remains unchanged (skill is NOT added as permanent participant)
- Multiple auto-invocations work independently without interference
- No errors occur during auto-invocation process

**Fail:**
- Skill is NOT invoked when user intent is clear
- Wrong skill is selected for the given intent
- Skill badge/icon does NOT appear or is not visible
- Skill is added as a permanent participant when it shouldn't be
- Error occurs during skill invocation or execution
- Multiple skills are invoked for a single request (when only one should be)
- Skill execution fails or returns irrelevant response

## Edge Cases

### Edge Case 1: Ambiguous Intent
**Test Input:** "Help me with this code"
**Expected:** System invokes the most relevant skill based on context, asks for clarification if too ambiguous, or defaults to general-purpose skill. No errors occur.

### Edge Case 2: No Matching Skill
**Test Input:** "What's the weather today?" (in project with only code-related skills)
**Expected:** No skill badge appears. System responds with regular chat or indicates no skill available. No errors occur.

### Edge Case 3: Multiple Matching Skills
**Setup:** Project has multiple skills that could handle code review
**Test Input:** "Review this code..."
**Expected:** System selects the MOST appropriate skill based on metadata confidence scores, priority/ranking, or historical usage. Only ONE skill is invoked (no duplicates).

### Edge Case 4: Skill Already Added as Participant
**Setup:** Add "code-reviewer" explicitly as a chat participant before test
**Test Input:** "Review this code..."
**Expected:** Skill executes (since it's already a participant). Badge still appears showing skill is active. No duplicate invocation occurs.

### Edge Case 5: Skill Invocation Failure
**Test Input:** Valid code review request, but skill fails internally
**Expected:** Error message is displayed clearly. User is informed that skill invocation failed. Chat remains functional. Option to retry or use different approach is available.

### Edge Case 6: Permission Restrictions
**Setup:** User lacks permission to use certain skills
**Test Input:** Request that would match a restricted skill
**Expected:** Skill is NOT invoked (respects permissions). Either a different permitted skill is used, or user is notified of permission restriction. No unauthorized skill execution occurs.

### Edge Case 7: Large Code Input
**Test Input:** Very large code block (>5000 characters) for review
**Expected:** System handles large input gracefully. Skill is invoked successfully. Performance remains acceptable. No truncation unless explicitly stated.

### Edge Case 8: Rapid Successive Messages
**Action:** Send multiple messages quickly: (1) "Review this code...", (2) "Also check this function...", (3) "And this class..."
**Expected:** Each message is processed independently. Skills are invoked appropriately for each. No race conditions or dropped invocations. Responses appear in correct order.

## Notes

- **Screenshot Evidence:** Capture screenshot when skill badge appears (reference: 2026-11-04_12h43_50.png showing "Skill: code-reviewer" badge)
- **Performance:** Note response time from message send to skill badge appearance (should be < 2 seconds for initial feedback)
- **Consistency:** Test multiple times to ensure consistent skill selection for same intent
- **Browser Compatibility:** Test in Chrome, Firefox, Safari, Edge if applicable
- **Mobile:** Verify auto-invocation works on mobile/tablet if platform supports it

## Related Test Cases

- TC-SKILL-EXPLICIT-001: Skill invocation with explicit participant
- TC-SKILL-METADATA-001: Skill metadata configuration and matching
- TC-CHAT-PERMISSIONS-001: Chat and skill permission validation
- TC-SKILL-BADGE-001: Skill badge UI rendering and behavior
- TC-SKILL-ERROR-001: Skill invocation error handling

## Defect Scenarios

If this test fails, potential defects include:
- **No Auto-Invocation:** Skill not invoked when user intent is clear
- **Wrong Skill Selected:** Inappropriate skill selected for given intent
- **No Visual Feedback:** Skill badge not displayed or not visible
- **Participant List Modified:** Skill added as permanent participant when it shouldn't be
- **Duplicate Invocations:** Multiple skills invoked for single request
- **Performance Degradation:** Significant delay or timeout with auto-invocation
- **Permission Bypass:** Restricted skills are invoked without proper permissions
- **Context Loss:** Previous skill invocations interfere with new ones
