---
id: ELITEA-0195
title: "TC-019: Warnings Do Not Block Publishing — Orange Advisory Banner but Publish Button Remains Enabled"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0195: TC-019: Warnings Do Not Block Publishing — Orange Advisory Banner but Publish Button Remains Enabled

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that warning-level validation issues produce an orange advisory banner while keeping the Publish button enabled — warnings are non-blocking advisories. The user can choose to publish despite warnings without being forced to fix them.

Coverage:
- Orange banner: "Your agent version meets the necessary requirements, but has some points for improvement. Follow summary details to improve."
- SUMMARY: Critical 0, Warnings > 0
- Publish button is enabled (cyan) when Critical 0, even if Warnings > 0
- Clicking Publish proceeds and the agent is published successfully
- Warning checks: welcome message missing toolkit reference, only 1 conversation starter, sub-agent description too short

## Preconditions

- Logged in as User A
- Agent E configured with warning-level deficiencies only (no critical issues):
  * Description: filled
  * Welcome message: does NOT mention toolkit configuration
  * Conversation starters: only 1 added
  * Sub-agent "DataFetcher": description is 3 words or fewer
  * All variables: have default values set

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Publish modal on Agent E; enter a valid unique version name; check 'I agree with the Publishing Terms.' | Continue button enabled |
| 2 | Click Continue | Validation step auto-triggers; spinner shown |
| 3 | Wait for validation to complete | Results appear |
| 4 | Observe the banner | Orange banner: 'Your agent version meets the necessary requirements, but has some points for improvement. Follow summary details to improve.' |
| 5 | Check SUMMARY section | Critical: 0, Warnings: > 0 (e.g., Warnings: 3) |
| 6 | Observe the Publish button | Publish button is cyan and enabled despite the presence of warnings |
| 7 | Read the warnings in SUMMARY DETAILS | Warnings include: 'Welcome message doesn’t mention toolkit configuration', 'Only 1 conversation starter (recommend 2+)', 'Sub-agent DataFetcher: Description is too short' |
| 8 | Click Publish | Publishing proceeds; success notification shown; agent published to Agents Studio despite warnings |

## Expected Final State

Publishing proceeds; success notification shown; agent published to Agents Studio despite warnings

## Pass/Fail Criteria

PASS:
- Orange banner shown with the advisory improvement message
- SUMMARY shows Critical: 0 with Warnings > 0
- Publish button is enabled when Critical is 0, regardless of warning count
- Clicking Publish succeeds — agent is published to Agents Studio
- Specific warnings listed include welcome message, conversation starters, and sub-agent description checks

FAIL:
- Orange banner not shown for warning-level issues
- Publish button is disabled due to warnings despite Critical being 0 (warnings incorrectly treated as blocking)
- Clicking an enabled Publish button fails or the agent is not published
- Warning entries are absent or do not match expected checks
