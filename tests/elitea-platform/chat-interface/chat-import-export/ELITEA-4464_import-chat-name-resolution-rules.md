---
id: ELITEA-4464
title: "Imported chat name is read from the file's internal content and matches the chat's actual renamed name, not the original first message or filename"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4464: Imported chat name is read from the file's internal content and matches the chat's actual renamed name, not the original first message or filename

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the imported chat name always derives from the chat's actual (renamed) name via the exported file's internal content — never from the downloaded filename, never from a stale first message — and that the export-timestamp suffix is stripped while any real date embedded in the chat's own name is preserved, names are truncated at 50 characters, and duplicate names are allowed.

---

## Preconditions

- None beyond standard chat creation and rename access.

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Chat A. Send the first message "Hi". Rename the chat to a name that includes characters disallowed in filenames, e.g. "Report?Q4:Summary/2026". Verify the chat list/header now shows exactly "Report?Q4:Summary/2026" (not "Hi"). | Chat A's name is now "Report?Q4:Summary/2026", confirming the name comes from the rename action, not the original first message. |
| 2 | Export Chat A "Without attachments". | Downloaded filename has every disallowed character (`? : /` etc.) from the renamed name replaced with `_`, e.g. `Report_Q4_Summary_2026_<YYYY-MM-DD_HH-mm-ss>.json` (or `.json.enc`). The filename is derived from the rename, not from "Hi". |
| 3 | Import Chat A's exported file into any project. | Imported chat's name is read from the file's internal content and shows exactly "Report?Q4:Summary/2026" — the original, unsanitized characters restored (sanitization only ever applied to the downloaded filename in step 2, never to the chat's actual name) — and is not "Hi". |
| 4 | Create Chat B. Send any first message. Rename it to "Daily sync 2026-10-01" (a real date intentionally embedded in the name). Export it, then import it. | Imported name is exactly "Daily sync 2026-10-01" — the real embedded date is kept; only the trailing export-timestamp suffix added to the downloaded filename is stripped (no over-stripping losing the real date, no under-stripping leaving the export timestamp too). |
| 5 | Create Chat C. Send any first message. Rename it to a string longer than 50 characters, e.g. "This is a very long chat name used specifically to test fifty character truncation behavior". Export it, then import it. | Import preview shows the name truncated to exactly the first 50 characters of the renamed name. |
| 6 | Create Chat D. Send any first message. Rename it to "From Ekaterina 2nd". Keep Chat D as-is in the target project (do not delete it). Create and export a second, independent chat also renamed to "From Ekaterina 2nd". Import that second chat's file, then import the same file again (a 3rd chat). | All imports succeed; all 3 chats (Chat D plus the 2 new imports) show the identical literal name "From Ekaterina 2nd", no "(1)"/"Copy of" suffix, no merge/overwrite; each has its own independent id; Chat D is unchanged. |

## Expected Final State

Chat naming always derives from the chat's actual (renamed) name via the file's internal content — never from the downloaded filename, never from a stale first message; suffix-vs-embedded-date distinction, length cap, and duplicate-name handling all work exactly as specified.

## Pass/Fail Criteria

**Pass:**
- All 6 steps match exactly as described.

**Fail:**
- Name derived from the original first message instead of the rename, name derived from filename, suffix over/under-stripped, wrong truncation point, or a duplicate-name import blocked/merged/suffixed.
