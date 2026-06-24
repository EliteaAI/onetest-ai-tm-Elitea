# Test Case Pattern Verification Report
**PR**: #22 - ELITEA-0001 to ELITEA-0033  
**Date**: 2026-06-25  
**Reviewer**: Claude Code QA

---

## Summary

Verified 33 test cases (ELITEA-0001 through ELITEA-0033) against OneTest TMS pattern standards. Found **format inconsistencies** between manually created files (0001-0006) and agent-created files (0007-0033).

---

## Reference Pattern (Correct Format)

Based on existing test case: `ELITEA-1370_ado42-delete-work-item.md`

```yaml
---
id: ELITEA-XXXX
title: "Quoted Title Text"
priority: critical|high|medium|low
type: functional|regression|smoke|integration
module: module-name
status: draft|ready|approved
execution_type: manual|automated
tags: [tag1, tag2, tag3]
requirements: [EliteaAI/repo#issue]
---
# ELITEA-XXXX: Title

**Module:** ModuleName · **Priority:** Level · **Type:** Type

**Objective:** One-line objective

## Preconditions

- Bulleted list
- No table format

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | ... | ... |

## Expected Final State

Description or structured data

## Pass/Fail Criteria

**Pass:**
- Condition 1
- Condition 2

**Fail:**
- Condition 1
- Condition 2
```

---

## Issues Found

### 1. **Title Quoting** ❌
- **Manual files (0001-0006)**: ✅ `title: "Quoted string"`
- **Agent files (0007-0033)**: ❌ `title: Unquoted string`
- **Impact**: YAML parsing may fail for titles with special characters
- **Fix Required**: Add quotes around all titles

### 2. **Status Field** ⚠️
- **Manual files (0001-0006)**: `status: draft`
- **Agent files (0007-0033)**: `status: approved`
- **Expected**: `status: draft` or `status: ready`
- **Impact**: Test cases marked as approved before QA review
- **Fix Required**: Change to `draft` or `ready`

### 3. **Tags Format** ❌
- **Manual files (0001-0006)**: ✅ `tags: [feat:personalization, r-2.0.4]`
- **Agent files (0007-0033)**: ❌ YAML list format:
  ```yaml
  tags:
    - personality
    - bare-persona
  ```
- **Expected**: Inline array format
- **Impact**: Inconsistent parsing, tag categorization broken
- **Fix Required**: Convert to inline array format

### 4. **Requirements Format** ❌
- **Manual files (0001-0006)**: ✅ `requirements: [EliteaAI/elitea_issues#5264]`
- **Agent files (0007-0033)**: ❌ YAML list with short reference:
  ```yaml
  requirements:
    - "#5394"
  ```
- **Expected**: Inline array with full repository path
- **Impact**: Traceability broken, issue linking fails
- **Fix Required**: Use full format `[EliteaAI/elitea_issues#5264]`

### 5. **Missing H1 Title** ⚠️
- **Reference pattern**: Has `# ELITEA-XXXX: Title` after frontmatter
- **Manual files (0001-0006)**: ❌ Missing H1
- **Agent files (0007-0033)**: ✅ Has H1 (but without ID prefix)
- **Expected**: `# ELITEA-XXXX: Title`
- **Impact**: Document structure incomplete
- **Fix Required**: Add proper H1 with ID prefix

### 6. **Missing Metadata Header** ⚠️
- **Reference pattern**: Has `**Module:** X · **Priority:** Y · **Type:** Z`
- **Manual files (0001-0006)**: ❌ Missing
- **Agent files (0007-0033)**: ❌ Missing
- **Expected**: Metadata header after H1
- **Impact**: Quick reference information not visible
- **Fix Required**: Add metadata header

### 7. **Missing Objective Section** ⚠️
- **Reference pattern**: Has `**Objective:** One-line description`
- **Manual files (0001-0006)**: ❌ Missing
- **Agent files (0007-0033)**: ❌ Missing
- **Expected**: Objective statement
- **Impact**: Test purpose unclear at glance
- **Fix Required**: Add objective section

### 8. **Test Data Format** ℹ️
- **Manual files (0001-0006)**: Uses table format
- **Agent files (0007-0033)**: Uses mixed format (bullets and tables)
- **Expected**: Either format acceptable
- **Impact**: None (style preference)
- **Action**: Standardize on table format for consistency

---

## Files Affected

### ✅ Correct Pattern (6 files)
Close to correct, but missing H1, metadata header, and objective:
- ELITEA-0001_verify-personalization-page-loads-with-default-personality-field.md
- ELITEA-0002_verify-bare-option-appears-in-default-personality-dropdown.md
- ELITEA-0003_select-bare-personality-and-verify-persistence-after-page-reload.md
- ELITEA-0004_verify-context-management-modal-opens-and-displays-bare-option.md
- ELITEA-0005_verify-bare-option-in-context-management-user-instructions-dropdown.md
- ELITEA-0006_create-chat-with-bare-personality-verify-raw-model-identity.md

### ❌ Pattern Issues (27 files)
Multiple format issues in frontmatter:
- ELITEA-0007.md through ELITEA-0033.md

---

## Recommended Actions

### Priority 1 - Critical Fixes (Blocks Parsing)
1. ✅ **Quote all titles** in files 0007-0033
2. ✅ **Convert tags to inline array format** `[tag1, tag2, tag3]`
3. ✅ **Fix requirements format** to `[EliteaAI/elitea_issues#5264]`

### Priority 2 - Important Fixes (Affects Workflow)
4. ✅ **Change status from `approved` to `draft`** in files 0007-0033
5. ✅ **Add H1 title with ID** to all 33 files: `# ELITEA-XXXX: Title`
6. ✅ **Add metadata header** to all 33 files

### Priority 3 - Enhancement (Best Practices)
7. ✅ **Add Objective section** to all 33 files
8. ✅ **Standardize Test Data format** to tables

---

## Next Steps

1. **Create corrective branch** from `add-tc/bare-personality-5264-0625-0233`
2. **Apply fixes** to all 33 test case files
3. **Update PR #22** with corrections
4. **Re-verify** against OneTest TMS standards
5. **Request review** from QA team

---

## Pattern Checklist

Use this checklist when creating new test cases:

```yaml
- [ ] Title is quoted
- [ ] Status is draft/ready (not approved)
- [ ] Tags use inline array format [tag1, tag2]
- [ ] Requirements use full path [EliteaAI/repo#issue]
- [ ] H1 title includes ID: # ELITEA-XXXX: Title
- [ ] Metadata header present
- [ ] Objective statement included
- [ ] Preconditions are bulleted (not table)
- [ ] Steps use table format
- [ ] Pass/Fail criteria use bold headers
```
