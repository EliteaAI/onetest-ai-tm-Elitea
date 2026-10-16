# Duplicate Chat Test Suite

**Feature:** Chat Duplication  
**GitHub Issue:** [#3837](https://github.com/EliteaAI/elitea_issues/issues/3837)  
**Related Bugs:** 
- [#6256](https://github.com/EliteaAI/elitea_issues/issues/6256) - All user participants not copied (only creator)
- [#6271](https://github.com/EliteaAI/elitea_issues/issues/6271) - Duplicated chat sorting issue

## Test Suite Overview

This test suite covers the **Duplicate Chat** functionality across Private Projects and Team Projects, validating participant handling, visibility states, and UI behavior.

### Test Case Range
- **IDs:** ELITEA-3928–ELITEA-3946 (12, renumbered from ELITEA-2616–2627 — see `CASE_ID_CHANGES.md`) and ELITEA-2628 to ELITEA-2640 (13) — 25 test cases
- **Total Lines:** 1,695

## Test Coverage

### 🔴 P0 - Core Duplication Behavior (9 test cases)
High priority tests covering essential duplication functionality.

| ID | Title | Key Validation |
|----|-------|----------------|
| ELITEA-3928 | Duplicate Chat from Context Menu | New independent chat created, original unchanged |
| ELITEA-3930 | Participants and Configuration Preserved | All participants copied (Bug #6256 validation) |
| ELITEA-3932 | Conversation Independence | Messages don't sync between original and duplicate |
| ELITEA-3934 | Persistence After Refresh | Both chats survive page reload |
| ELITEA-3936 | Pinned Chat Duplication | Duplicate unpinned, original remains pinned |
| ELITEA-3938 | Public Chat Visibility Preserved | Duplicate inherits public state (green indicator) |
| ELITEA-3940 | Public Visibility to All Team Members | Duplicate visible to non-participants |
| ELITEA-3942 | Nested Public Chat Duplication | Public state preserved through multiple duplications |
| ELITEA-3943 | Access Control Security | No unauthorized data exposure |

### 🟡 P1 - Participant Handling & Visibility (12 test cases)
Medium priority tests for participant management and visibility rules.

| ID | Title | Key Validation |
|----|-------|----------------|
| ELITEA-3944 | AI Participants Only (Private) | Agent/Pipeline/Toolkit/MCP preserved |
| ELITEA-3945 | AI Configuration Retained | AI participant settings intact |
| ELITEA-3946 | No Unintended User Addition | AI-only chats stay AI-only |
| ELITEA-2628 | Mixed Participants (Users + AI) | All participant types preserved |
| ELITEA-2629 | No Participant Crossover | Only original participants copied |
| ELITEA-2630 | Restrictions Persist | Access control after refresh/API |
| ELITEA-2631 | Original Public Indicator | Green indicator on original |
| ELITEA-2632 | Duplicate Public Indicator | Green indicator on duplicate |
| ELITEA-2633 | Private Chat Remains Private | No auto-public conversion |
| ELITEA-2634 | Visibility Independence | Changes don't affect each other |
| ELITEA-2635 | Original Chat Integrity | All properties unchanged after duplication |
| ELITEA-2636 | Naming Convention | Unique names with "Copy of" or numbering |

### 🟢 P2 - UI and Regression Coverage (4 test cases)
Low priority tests for UI behavior and edge cases.

| ID | Title | Key Validation |
|----|-------|----------------|
| ELITEA-2637 | Inaccessible AI State | Clear error indicators, no silent access |
| ELITEA-2638 | Context Menu UI | Duplicate action visible and positioned |
| ELITEA-2639 | Chat List Sorting (Bug #6271) | Duplicate at top of list |
| ELITEA-2640 | Participant Panel Rendering | No UI regression for all participant types |

## Test Contexts

### Private Project
- Single user (owner only)
- AI participants only: Agent, Pipeline, Toolkit, MCP
- No user participants can be added

### Team Project
- Multiple users available
- Can have user participants
- Can have AI participants
- **Public chats (green indicator):** Visible to all team members
- **Non-public chats:** Visible only to participants

## Key Validations

### Bug #6256 Fix
**Issue:** Duplicated chat only copied creator, not all user participants  
**Validation:** ELITEA-3930, ELITEA-2628  
**Expected:** ALL user participants copied to duplicate

### Bug #6271 Fix
**Issue:** Duplicated chat not sorted above original  
**Validation:** ELITEA-2639  
**Expected:** Duplicate appears at top of list (most recent)

## Public vs Non-Public Chats

### Public Chats (Green Indicator 🟢)
- Marked with green color/indicator
- Visible to ALL team members (not just participants)
- Visibility inherited by duplicate
- Tests: ELITEA-3938, 3940, 3942, 2631, 2632

### Non-Public Chats
- No green indicator
- Visible only to participant users
- Privacy inherited by duplicate
- Tests: ELITEA-2633, 2634

## Execution Priority

1. **Start with P0 tests** - Core functionality must work
2. **Run P1 tests** - Participant and visibility handling
3. **Complete with P2 tests** - UI polish and edge cases

## Related Documentation

- **Feature Ticket:** https://github.com/EliteaAI/elitea_issues/issues/3837
- **Bug #6256:** https://github.com/EliteaAI/elitea_issues/issues/6256
- **Bug #6271:** https://github.com/EliteaAI/elitea_issues/issues/6271

---

**Generated:** 2026-08-18  
**Test Suite Version:** 1.0  
**Status:** Ready for execution
