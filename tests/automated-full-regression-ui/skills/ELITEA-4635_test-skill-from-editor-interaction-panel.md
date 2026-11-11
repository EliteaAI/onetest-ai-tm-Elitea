---
id: ELITEA-4635
title: "ELITEA-4635: Test Skill from Editor via Test Skill Button and Verify Execution"
priority: critical
type: regression
module: skills
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.skills.test_skill_editor_test_button_execution.TestSkillEditorTestButtonExecution.test_test_skill_button_opens_panel_and_executes_skill
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/9e4121eb1b8a27ae0e896857e4238f1294a24ad6
tags: [automated:UI:regression, feat:skills, test-panel, skill-execution]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4635: Test Skill from Editor via Test Skill Button and Verify Execution

**Module:** Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that users can test a skill directly from the skill editor page using the "Test Skill" button, which opens an interaction panel where they can send a message, observe the skill execution with visible execution steps (skill being added), and receive a response without errors.

**Coverage:**
- Test Skill button visible and clickable in skill editor
- Interaction panel/window opens on click
- User can enter and send test message
- Execution steps display (showing skill being added to execution)
- Skill processes message successfully
- Response received without errors
- Complete test workflow from editor

## Preconditions

- User is logged into {{base_url}}
- User has navigated to Skills page (click "Skills" in left sidebar)
- User has clicked on a skill to open the skill editor (e.g., "lmt-answer-format")
- Skill editor page is displayed with skill details

## Test Data

| Field | Value |
|-------|-------|
| Skill name | lmt-answer-format (or any available skill) |
| Test message | "run" (or any simple instruction) |
| Expected | Skill executes and returns formatted response |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On the skill editor page, locate the "Test Skill" button in the top toolbar | "Test Skill" button is visible (next to "Edit with AI" button) |
| 2 | Click the "Test Skill" button | An interaction panel/window opens on the right side of the screen |
| 3 | Observe the interaction panel interface | Panel displays with an input field at the bottom, placeholder text "Type your message...", and send button (arrow icon) |
| 4 | Type a test message in the input field: "run" | Text "run" appears in the input field |
| 5 | Click the send button (arrow icon →) or press Enter | Message sends successfully |
| 6 | Observe the execution process | Message appears in the interaction panel thread with user avatar/name |
| 7 | Wait for skill processing | "Thought for X secs" indicator appears showing skill is processing |
| 8 | Observe execution steps/details | Execution steps display showing skill being added (e.g., "Skill: lmt-answer-format" tag/badge appears) |
| 9 | Verify execution context shows the skill | In the interaction panel, under the response or in execution details, skill name badge appears (e.g., "Skill: lmt-answer-format" with tool icon and model info like "Bedrock GPT-5.6-Luna") |
| 10 | Wait for response completion | Skill completes processing |
| 11 | Verify response appears in interaction panel | Response from skill displays in the panel thread |
| 12 | Verify response content is relevant | Response matches skill's purpose (e.g., formatted answer according to skill instructions) |
| 13 | Verify no error messages displayed | No error messages or failure indicators visible in the response |
| 14 | Verify execution completed successfully | Execution shows successful completion status (no error icons or warnings) |

## Expected Final State

- Test Skill button opens functional interaction panel
- User successfully sent test message
- Skill executed with visible execution steps showing skill was added
- Response received without errors
- Execution details show skill name and model used
- Complete test cycle completed within the skill editor interface

## Pass/Fail Criteria

**Pass:**
- Test Skill button opens interaction panel
- Message sends successfully from panel
- Execution steps display showing skill being added to execution
- Skill processes message and returns response
- No errors displayed in execution or response
- Response content is relevant to skill's instructions
- Execution completed successfully indicator shown

**Fail:**
- Test Skill button doesn't open interaction panel
- Cannot send message from interaction panel
- No execution steps or skill execution details visible
- Skill doesn't execute or times out
- Error messages displayed in execution
- Response is error message or irrelevant
- Execution shows failure status

## Notes

**Source functional tests:** Based on ELITEA-4240, ELITEA-4242 functionality but executed from skill editor Test panel
**Regression rationale:** Critical workflow for skill developers to test their skills directly from the editor; validates interaction panel functionality, execution visibility, and successful skill runs.
**Selected checkpoints:** Test Skill button, interaction panel display, message send, execution steps visibility (skill being added), response receipt without errors.
**UI Context:** Based on skill editor interface with Test Skill button in top toolbar, interaction panel on right side with execution steps showing "Skill: {skill-name}" badge.
