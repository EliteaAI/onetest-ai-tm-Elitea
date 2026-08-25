---
id: ELITEA-2770
title: "Edit with AI modal displays header and text input for natural language request"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent's configuration page is open

## Test Data

| Field | Value |
|-------|-------|
| Sample prompt | "Improve this agent" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and click "Edit with AI" CTA | Modal opens |
| 2 | Verify the modal displays a visible header | Header text is present and readable |
| 3 | Verify a text input field is displayed for the natural language request | Text input is visible |
| 4 | Type a sample prompt into the text field | Typed text appears in the field |
| 5 | Verify a "Generate Draft" (or similarly labeled) button is available | Submit button present and enabled once text is entered |

## Expected Final State

The Edit with AI modal is fully rendered with a header, a functional text input, and an available submit control, ready to accept a prompt.

## Pass/Fail Criteria

**Pass:**
- Header, text input, and submit button are all present and functional on modal open

**Fail:**
- Header is missing, the text input does not accept typed input, or no submit control is available
