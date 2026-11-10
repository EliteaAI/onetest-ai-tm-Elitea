---
id: ELITEA-4470
title: "Deselected or unavailable attachments show the exact (not imported) placeholder text in context; zero-selection still allows import"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4470: Deselected or unavailable attachments show the exact (not imported) placeholder text in context; zero-selection still allows import

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that deselected or unavailable attachments always show the exact `(not imported)` placeholder text in their original message position, in whichever of the two observed wording forms actually appears, and that importing with zero attachments selected still succeeds.

**Note on exact wording:** the placeholder text for a deselected/unavailable attachment can appear in more than one form depending on the surrounding message context — report exactly which form appears, do not assume:
- When the original attachment message included wording like "sent while running" before the file reference (e.g. a tool-call-in-progress style message): the placeholder appears as `sent while running📎 <name> (not imported)`.
- When the original attachment message was a plain generated-file announcement (e.g. "Created these files in the bucket: ..."): the placeholder appears as plain `📎 <name> (not imported)`, inline with the rest of that message's text.

---

## Preconditions

- Create Chat A: a first message that causes a response to reference 5 distinct attachments (e.g. ask the AI to summarize/attach 5 different files it has access to). Export "With attachments".
- Create Chat B: a message where an agent/tool generates 2 files and announces them in a single response (e.g. "Created these files in the bucket: - `<file1>` — ... - `<file2>` — ..."). Export "With attachments".

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Import Chat A's export, deselecting 3 of the 5 attachments, keeping 2 selected. | The deselected 3 each show, exactly, their observed placeholder form ending in `(not imported)`, with no download link, in their original message position. The 2 kept-selected attachments show as downloadable and work correctly. |
| 2 | Import Chat A's export again, this time unchecking "Select all" entirely. | Import still succeeds (not blocked); all 5 attachments show the `(not imported)` placeholder; chat imports with messages only. |
| 3 | Import Chat B's export, deselecting both of the 2 attachments. | The message shows both filenames inline, each suffixed `(not imported)`, no download link — matching the exact text of the original announcement message plus the two placeholders appended. |
| 4 | Import Chat A's export a second time (a new, independent chat). Compare one of the kept-selected attachments across both resulting chats. | Filename and content identical and correct in both — no cross-talk, no collision. |

## Expected Final State

Attachment selection state is always honored precisely including zero-selection; the placeholder always ends in `(not imported)` with no download link, with wording that depends on message context.

## Pass/Fail Criteria

**Pass:**
- Placeholder text matches one of the two documented forms exactly; selected files always remain downloadable; zero-selection import is never blocked.

**Fail:**
- Wrong/missing placeholder text, a selected file not downloadable, or a blocked zero-selection import.

**Note (flagged, not a bug by itself):** the issue's written spec only describes the plain `📎 <name> (not imported)` form — the "sent while running" prefix variant is real shipped behavior not mentioned in the spec. Worth a one-line mention if ever reporting findings, not something to fail this test case over.
