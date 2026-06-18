---
id: ELITEA-0491
title: "Verify Programming File Accepted in Chat Conversation - Extended File Types"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, story:3671, r-2.0.1, chat]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0491: Verify Programming File Accepted in Chat Conversation - Extended File Types

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the full set of supported programming file types from the issue requirements (.cpp, .c, .h, .cs, .go, .rb, .php, .swift, .kt, .rs, .sql, .sh) are accepted by the attachment system when the backend includes them in `code_types`.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation is open (LLM/direct chat)
3. The backend API returns all required extensions in `code_types` for the current project
4. Sample files are available for each extension listed in TEST DATA

## Test Data

- `calculator.cpp`: C++ source file (~1KB)
- `utils.c`: C source file (~500 bytes)
- `types.h`: C header file (~500 bytes)
- `Program.cs`: C# source file (~1KB)
- `main.go`: Go source file (~500 bytes)
- `helper.rb`: Ruby script (~500 bytes)
- `api.php`: PHP file (~500 bytes)
- `AppDelegate.swift`: Swift file (~1KB)
- `Activity.kt`: Kotlin file (~1KB)
- `lib.rs`: Rust file (~500 bytes)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation | Conversation is displayed with attachment button |
| 2 | Click the attachment button and select `calculator.cpp` | `calculator.cpp` attaches successfully; no error toast shown |
| 3 | Click attachment button and select `utils.c` | `utils.c` attaches; total count 2 |
| 4 | Click attachment button and select `types.h` | `types.h` attaches; total count 3 |
| 5 | Click attachment button and select `Program.cs` | `Program.cs` attaches; total count 4 |
| 6 | Click attachment button and select `main.go` | `main.go` attaches; total count 5 |
| 7 | Click attachment button and select `helper.rb` | `helper.rb` attaches; total count 6 |
| 8 | Click attachment button and select `api.php` | `api.php` attaches; total count 7 |
| 9 | Click attachment button and select `AppDelegate.swift` | `AppDelegate.swift` attaches; total count 8 |
| 10 | Click attachment button and select `Activity.kt` | `Activity.kt` attaches; total count 9 |
| 11 | Click attachment button and select `lib.rs` | `lib.rs` attaches; total count 10 (max reached) |

## Expected Final State

`lib.rs` attaches; total count 10 (max reached)

## Pass/Fail Criteria

- PASS: Each file type attaches without an "Invalid file types" error; all files appear in the attachment list; attachment count reaches 10 at step 11
- FAIL: Any file triggers an invalid type error; any file is silently dropped; attachment count does not increment
