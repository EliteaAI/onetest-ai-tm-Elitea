---
id: ELITEA-4524
title: "Verify web_extract Urls field (JSON array editor) validates boundary and malformed input correctly"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid API key, open on its "Test Toolkit" page, Web extract selected

## Test Data

| Case | Value |
|------|-------|
| Exactly at limit | 5 valid URLs as a JSON array |
| Over limit | 6 valid URLs |
| Empty | `[]` |
| Non-http/https | `["ftp://example.com/file"]` |
| Malformed JSON | A trailing comma or unclosed bracket |
| Duplicate URL | Same URL listed twice |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enter exactly 5 valid URLs and run | Run succeeds |
| 2 | Enter exactly 6 valid URLs and run | Clean message stating the limit (e.g. "At most 5 URLs per call"), not a raw error |
| 3 | Enter `[]` and attempt to run | "Run Test" is disabled (Urls required), or if clickable, a clear validation message is returned rather than a raw exception or silent acceptance |
| 4 | Enter a single non-http/https URL and run | Clean rejection message stating only http/https URLs are allowed, not a raw exception |
| 5 | Enter malformed JSON | Editor's inline syntax indicator blocks submission, or a clear error is returned if submission proceeds |
| 6 | Enter the same URL twice and run | Either deduplicated silently or processed without error; document which |

## Expected Final State

The Urls field correctly enforces its 5-URL limit, http/https-only rule, and JSON validity, with clean messaging throughout.

## Pass/Fail Criteria

**Pass:**
- All boundary and malformed-input cases produce clean, documented behavior with no raw exceptions

**Fail:**
- Any case produces a raw exception, silently accepts an invalid state, or crashes the Test page
