---
id: ELITEA-4475
title: "Export's missing-file count/toast and Import's exact placeholder text remain correct (bug #7208 fix)"
priority: critical
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-export, chat-import, regression, bugfix, issue:6903, issue:6904, issue:7208, p0]
requirements: ["EliteaAI/elitea_issues#6903", "EliteaAI/elitea_issues#6904", "EliteaAI/elitea_issues#7208"]
---

# ELITEA-4475: Export's missing-file count/toast and Import's exact placeholder text remain correct (bug #7208 fix)

**Module:** chat-interface · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm the fix for the previously intermittent stale-count bug (#7208) holds: Export's missing-file label/toast and Import's exact placeholder text remain correct. This bug was intermittent before the fix (2 of 4 attempts failed) — repeat at least 2-3 times before concluding Pass.

---

## Preconditions

- Create a chat where an agent/tool generates 2 files directly into the Artifacts bucket as part of its response.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Delete 1 of the 2 generated files directly from the Artifacts bucket (not via the chat message's delete button). Open Export modal, "With attachments". | Label shows the real, storage-verified count including "unavailable", e.g. "With attachments (1 file · <size> · 1 unavailable)" — not a stale count. |
| 2 | Export. | Warning toast "Chat exported. 1 file(s) could not be included." appears. |
| 3 | Import the file. | The missing attachment shows "Not available in archive", correctly excluded from the selection counter; completing import shows it as "<name> (not imported)" in place. |

## Expected Final State

The fix holds with exact label/toast/placeholder text, no regression to the previously-intermittent stale-count bug.

## Pass/Fail Criteria

**Pass:**
- All quoted text matches exactly across at least 2-3 repeated attempts (fresh files each time).

**Fail:**
- Any stale count, wrong/missing toast, or incorrect Import-side label/placeholder on any attempt.
