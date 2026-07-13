---
id: ELITEA-1876
title: "Run history panel shows past runs with timestamp and preview"
priority: high
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1876: Run history panel shows past runs with timestamp and preview

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the run history panel opens correctly and displays past chat runs with both a timestamp and a conversation preview for each entry.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.
- At least one message has been sent in the embedded chat panel to generate a run history entry.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Send at least one message in the embedded chat panel | The message is sent and a response is received |
| 3 | Locate the run history icon (clock icon) and click it | The run history panel opens |
| 4 | Verify the run history panel opens | The run history panel is visible |
| 5 | Verify at least one entry is listed | At least one run history entry is present |
| 6 | Verify each entry shows: a timestamp and a preview of the conversation (first message or title) | Every listed entry displays a timestamp and a conversation preview |

---

## Expected Final State

The run history panel is open and shows at least one entry, each with a timestamp and a conversation preview.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Run history panel opens and lists entries with timestamps and conversation previews.

**Fail:**
- Any step produces an error or unexpected result.
- The panel does not open, shows no entries, or entries are missing timestamps or previews.
