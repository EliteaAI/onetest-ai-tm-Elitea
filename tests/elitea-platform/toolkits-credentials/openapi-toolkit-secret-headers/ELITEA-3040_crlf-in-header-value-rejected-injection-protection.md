---
id: ELITEA-3040
title: "CRLF/Newline in a Header Value Is Rejected — Header-Splitting/Injection Protection"
priority: high
type: security
module: openapi-toolkit-secret-headers
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6002, nfr:security, nfr:validation, new]
requirements: [EliteaAI/elitea_issues#6002]
---

# ELITEA-3040: CRLF/Newline in a Header Value Is Rejected — Header-Splitting/Injection Protection

**Module:** Toolkits & Credentials / OpenAPI Toolkit Secret Headers · **Priority:** High · **Type:** Security

**Objective:** Confirm `OpenApiConfiguration`'s validator explicitly blocks CR/LF sequences inside a header value — this is a header-splitting/injection protection. Attempt to enter a value containing a CRLF sequence and confirm it is rejected at save time; if the input control itself strips newlines client-side before the value ever reaches save, document that as the observed mechanism instead.

---

## Preconditions

- Logged in to `{{base_url}}` with permission to create/edit an OpenAPI credential.
- A way to paste multi-line/CRLF content into the header value field (e.g. clipboard paste, since typing Enter may be intercepted by the form).

---

## Test Data

| Field | Value |
|-------|-------|
| Header name | `X-Custom` |
| Header value (paste) | `line1\r\nInjected-Header: x` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Add a header row, set name to `X-Custom`. | Row accepts the name. |
| 2 | Paste `line1\r\nInjected-Header: x` into the value field. | Document what actually happens: value accepted as-is, newline visibly stripped by the input control, or paste rejected outright. |
| 3 | Attempt to save. | If the CRLF reached the save request unmodified, the save must be rejected with a clear validation error (server-side protection). If the client already stripped the CRLF before save, the save may succeed with the stripped (single-line) value — document which path was observed. |
| 4 | Confirm no header with an embedded CRLF is ever persisted, regardless of which path (client-strip vs. server-reject) was taken. | No stored header value contains a raw CR or LF character. |

---

## Expected Final State

A CRLF-injection attempt in a header value can never reach persisted storage, whether blocked client-side or server-side.

---

## Pass/Fail Criteria

**Pass:** The CRLF sequence is neutralized — either stripped before save or rejected by the server-side validator — and no persisted header value contains a raw CR/LF.
**Fail:** A header value containing a raw CRLF sequence is successfully saved and persisted.
