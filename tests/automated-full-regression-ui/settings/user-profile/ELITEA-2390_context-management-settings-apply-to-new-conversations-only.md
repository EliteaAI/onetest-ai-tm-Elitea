---
id: ELITEA-2390
title: "Context Window Mode Settings Apply to New Conversations Only"
priority: high
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings, feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

# ELITEA-2390: Context Window Mode Settings Apply to New Conversations Only

**Module:** settings-user-profile · **Priority:** high · **Type:** functional

**Rewrite note (2026-11-12):** Original case set numeric "Max Context Tokens=32000" / "Preserve Recent Messages=3" values, which no longer exist per EliteaAI/elitea_issues#6898. Rewritten around the new Context window mode (Balanced/Full), which per AC3's ticket correction is a single personal setting applied across all projects — "new conversations only" here means new vs. existing *conversations*, not new vs. existing *projects* (that isolation was explicitly removed from the ticket; see ELITEA-4672 in this repo for the project-consistency check).

**Objective:** Verify that changing the personal Context window mode affects only newly created conversations, not existing ones.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Context window mode | Full |
| Preserve Recent Messages | 3 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Select "Full" and set Preserve Recent Messages to 3 | Action completes without error and produces the expected UI state. |
| 3 | Navigate away and back to confirm values were auto-saved | Target page/section loads successfully. |
| 4 | Create a new conversation | Operation completes successfully. |
| 5 | Verify the new conversation shows Window: Full with the configured Preserve Recent Messages value | Condition holds as described. |
| 6 | Open a previously existing conversation (created before this change) | Target page/section loads successfully. |
| 7 | Verify its Context Management settings remain unchanged from before | Condition holds as described. |

---

## Expected Final State

New conversations inherit the updated personal setting; pre-existing conversations are unaffected.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- New conversation reflects the updated mode; existing conversation's settings are unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- Either conversation's settings diverge from expected.
