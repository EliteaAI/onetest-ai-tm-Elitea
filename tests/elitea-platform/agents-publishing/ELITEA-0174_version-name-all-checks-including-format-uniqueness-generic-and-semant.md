---
id: ELITEA-0174
title: "Version Name — All Checks Including Format, Uniqueness, Generic, and Semantic Hint (Code-Based)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0174: Version Name — All Checks Including Format, Uniqueness, Generic, and Semantic Hint (Code-Based)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that all code-based validation rules for the version name are applied correctly across Critical, Warning, and Info/Suggestion severity levels during publishing. Checks run deterministically without LLM usage.

## Preconditions

Agent exists with at least one previously published version and one saved version. Publish modal is accessible.

**Test Data:**

| Row | Input Value | Check Section | Expected Severity | Expected Finding |
|-----|-------------|---------------|-------------------|------------------|
| 1 | (empty) (only by API) | Critical issues | ERROR| String should match pattern '^[a-zA-Z0-9._-]{1,50}$' |
| 2 | Name with unsupported special characters (e.g. "v1.0 beta!", "release@2025") (only by API) | Critical issues | ERROR | Invalid format: only alphanumeric, dots, hyphens, underscores allowed (1–50 chars) (String should match pattern '^[a-zA-Z0-9._-]{1,50}$') |
| 3 | String exceeding 50 characters (only by API) | Critical issues | ERROR | Invalid format: name exceeds 50 characters (String should match pattern '^[a-zA-Z0-9._-]{1,50}$') |
| 4 | Name identical to an existing published OR saved version of this agent (only by API) | Critical issues | Critical | Version name must be unique within the project/app |
| 5 | Generic version name from blocklist (e.g. "v1", "v2") | Warnings | Warning | Version name is generic; consider a more descriptive name |
| 6 | Valid version name that does not follow semantic versioning (e.g. "release-jan") | Suggestions | Info | Consider using semantic versioning (e.g. 1.0.0) |
| 7 | Valid semantic version, unique, within length limit (e.g. "1.2.0") | All sections | None | No issue raised |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click Publish | Publish modal opens |
| 2 | Enter the version name from Row 1 of the Test Data table | Version name field populated |
| 3 | Accept the agreement, click Publish | Validation runs; results panel shown |
| 4 | Check the section listed for Row 1 (Critical issues) | Version name flagged as Critical: version name is empty |
| 5 | Repeat steps 1–4 for Rows 2 through 7, entering the version name from the Test Data table per row | Row 2: Critical (invalid chars); Row 3: Critical (too long); Row 4: Critical (not unique); Row 5: Warning (generic blocklist); Row 6: Info/Suggestion (not semver); Row 7: absent from all sections |

## Expected Final State

Row 2: Critical (invalid chars); Row 3: Critical (too long); Row 4: Critical (not unique); Row 5: Warning (generic blocklist); Row 6: Info/Suggestion (not semver); Row 7: absent from all sections

## Pass/Fail Criteria

Pass: All rows produce the expected severity level; Row 7 (valid semantic version) produces no issue.
Fail: Any row missing its expected finding; severity mismatch; valid version name incorrectly flagged.
