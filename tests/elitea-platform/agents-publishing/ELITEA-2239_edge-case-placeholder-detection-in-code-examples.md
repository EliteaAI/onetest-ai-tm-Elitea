---
id: ELITEA-2239
title: "Edge case - placeholder detection in code examples"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with publish permissions
- Test agent created for edge case testing
- Skill with placeholder text inside code example prepared

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill Name | "Code Example Skill" |
| Skill Content | "When reviewing code, look for incomplete sections. Here is an example: `// TODO: implement validation`. Also watch for markers like [REPLACE] in templates. Help developers identify these placeholder sections." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attach "Code Example Skill" to test agent | Skill attached |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for validation | Result: **FAIL** |
| 4 | Verify CRITICAL finding for "TODO" | Finding: Placeholder text detected (TODO) |
| 5 | Verify CRITICAL finding for "[REPLACE]" | Finding: Placeholder text detected ([REPLACE]) |
| 6 | Verify **Publish** button state | Button **disabled** |
| 7 | Fix Skill: remove or rephrase placeholder keywords | Replace "TODO" with "unfinished task marker", "[REPLACE]" with "substitution marker" |
| 8 | Re-run validation | Result: **PASS** |

## Expected Final State

Placeholder keywords produce CRITICAL findings regardless of context (even inside code examples or quoted text). Validation is pattern-based, not context-sensitive.

## Pass/Fail Criteria

**Pass:**
- Placeholder keywords produce CRITICAL findings regardless of context
- TODO inside code example → CRITICAL
- [REPLACE] inside quoted text → CRITICAL
- Validation is pattern-based, not context-sensitive
- After removing placeholder keywords, validation passes

**Fail:**
- Placeholders in code examples not detected
- Context-aware detection allows placeholders in certain contexts
