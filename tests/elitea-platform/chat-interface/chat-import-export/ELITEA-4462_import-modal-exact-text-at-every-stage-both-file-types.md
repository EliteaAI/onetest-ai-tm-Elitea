---
id: ELITEA-4462
title: "Import modal shows exact specified text at every stage, for both a JSON-only and a ZIP-with-attachments file"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4462: Import modal shows exact specified text at every stage, for both a JSON-only and a ZIP-with-attachments file

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the Import modal's exact text at the initial, checking, JSON-only-preview, ZIP-preview, and importing-progress stages, for both file types.

---

## Preconditions

- Create Chat A: first message "Suggest?popular:armenian/song", no other messages, no attachments. Export it "Without attachments" — this is the JSON-only file used below.
- Create Chat B: first message that results in exactly 5 distinct uploaded or generated attachments in the chat (e.g. upload or generate 5 differently-named files across the conversation). Export it "With attachments" — this is the ZIP file used below.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chats header. | Import button beside Search, tooltip "Import" on hover; icon-only when sidebar collapsed/window narrow. |
| 2 | Click Import. | Modal shows exactly: "Import chat" / "Select an encrypted chat file exported from ELITEA (.json.enc or .zip.enc), or drop it here." / "Choose file" button. Cancel and Import buttons present; Import disabled. |
| 3 | Press Esc / click X / click Cancel, each without selecting a file. | Modal closes cleanly each time, no chat created. |
| 4 | Select Chat A's exported JSON file. | Filename shown; "Change file" button disabled; a "checking file" loading line is shown while validating. |
| 5 | Wait for validation. | "Change file" re-enables. Preview shows exactly: "File checked successfully" / "Chat name: Suggest?popular:armenian/song" / "Messages: 1 messages" (or the actual count sent) / "Exported at: <date/time>" / "This chat will be imported without attachments." |
| 6 | Select Chat B's exported ZIP file instead. | After checking, preview shows: "File checked successfully" / "Chat name: <Chat B's auto-derived name>" / "Messages: <N> messages" / "Exported at: <date/time>" / "Select all" / one row per attachment (name, size, Uploaded/Generated type) / "Selected 5 of 5 attachments (<total size>)" — the total size shown must equal the sum of all 5 individual file sizes. |
| 7 | Uncheck exactly one attachment row. | Counter updates to "Selected 4 of 5 attachments" with reduced size; "Select all" reflects the partial state. |
| 8 | Uncheck "Select all" entirely. | Counter reads "Selected 0 of 5 attachments (0 Bytes)". |
| 9 | Re-check all, click Cancel at this preview step, then reopen Import. | Modal closes, staged import discarded; reopening starts fresh. |
| 10 | Click Import. | Progress shown, exactly: "Importing chat... Uploading <N> attachment(s)" (N = however many were actually selected), with Cancel and an "Importing..." loading-state button. Attempt to close via X/click-outside/Esc during this step — modal does NOT close. |
| 11 | Wait for completion. | Modal closes automatically; new chat opens/selected; no "Imported" badge anywhere on it. |

## Expected Final State

Every modal stage shows exactly the specified text, for both a JSON-only and a 5-attachment ZIP file.

## Pass/Fail Criteria

**Pass:**
- Every quoted line matches exactly at every step; the attachment total-size sum is numerically correct.

**Fail:**
- Any wording mismatch, wrong counts, incorrect size sum, or the modal closing mid-commit.
