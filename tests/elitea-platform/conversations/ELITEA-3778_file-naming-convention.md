---
id: ELITEA-3778
title: "Verify Exported File Naming Convention"
priority: high
type: functional
module: conversations
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, feat:export, r-2.0.8]
requirements: [EliteaAI/elitea_issues#4590]
---
# ELITEA-3778: Verify Exported File Naming Convention

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that exported files follow the correct naming pattern: `Conversation_[Name]_YYYY-MM-DD` with appropriate extension (.json or .zip).

**Coverage:**
- Filename starts with "Conversation_"
- Conversation name included in filename
- Date in YYYY-MM-DD format (today's date)
- Correct extension (.json or .zip)
- Special characters handled properly
- Spaces replaced appropriately

## Preconditions

- Logged in to {{base_url}}
- Multiple conversations with different names
- User is the conversation creator

## Test Data

- Conversation 1: "Project Planning"
- Conversation 2: "Bug Triage"
- Conversation 3: "Meeting Notes" (test with/without attachments)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Export "Project Planning" without attachments | JSON file downloads |
| 2 | Verify filename format | Format: `Conversation_Project_Planning_2026-10-19.json` (or similar with today's date) |
| 3 | Check filename components - Prefix | Starts with "Conversation_" |
| 4 | Check filename components - Name | Includes "Project_Planning" (spaces replaced with underscores) |
| 5 | Check filename components - Date | Includes "2026-10-19" (YYYY-MM-DD format, today's date) |
| 6 | Check filename components - Extension | Extension: .json |
| 7 | Export "Bug Triage" with attachments | ZIP file downloads |
| 8 | Verify ZIP filename format | Format: `Conversation_Bug_Triage_2026-10-19.zip` |
| 9 | Check ZIP filename components | Prefix: "Conversation_", Name: "Bug_Triage", Date: "2026-10-19", Extension: .zip |
| 10 | Export "Meeting Notes" without attachments | JSON file downloads |
| 11 | Verify filename | Format: `Conversation_Meeting_Notes_2026-10-19.json` |
| 12 | Test conversation with special characters (if available) | e.g., "Test: Q&A Session" |
| 13 | Verify special character handling | Special characters (: & etc.) replaced or removed, safe filename generated |
| 14 | Export same conversation twice on same day | Both files download |
| 15 | Verify duplicate handling | Second file has suffix "(1)" or timestamp, e.g., `Conversation_Project_Planning_2026-10-19(1).json` or similar |

## Expected Final State

- All exported files follow naming pattern: `Conversation_[Name]_YYYY-MM-DD.ext`
- Date matches today's date
- Extension correct (.json or .zip)
- Special characters handled safely

## Pass/Fail Criteria

**Pass:**
- All files start with "Conversation_"
- Conversation name included (spaces replaced with underscores or removed)
- Date in YYYY-MM-DD format (today's date)
- Correct extension (.json for without attachments, .zip for with attachments)
- Special characters handled (replaced/removed)
- Duplicate exports handled (no overwrite or clear differentiation)

**Fail:**
- Filename doesn't start with "Conversation_"
- Conversation name missing or incorrect
- Date wrong format or incorrect date
- Wrong extension
- Special characters cause errors
- Duplicate exports overwrite without warning

## Postconditions

- All exported files have valid, unique filenames
- Files easily identifiable by name and date
