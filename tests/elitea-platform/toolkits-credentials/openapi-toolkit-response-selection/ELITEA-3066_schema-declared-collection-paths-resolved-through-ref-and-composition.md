---
id: ELITEA-3066
title: "Schema-Declared Collection Paths Are Resolved Through $ref/allOf/anyOf/oneOf Composition"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, needs-fixture]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3066: Schema-Declared Collection Paths Resolved Through $ref/allOf/anyOf/oneOf Composition

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm collection discovery correctly resolves the response collection when the OpenAPI schema declares it indirectly — via `$ref`, or composed with `allOf`/`anyOf`/`oneOf`/`additionalProperties` — rather than as a direct inline array. **Not covered by this session's live public-API pass** — none of the tested public APIs (GitHub Search, VSCode issues, REST Countries, PokeAPI, httpbin) exposed an OpenAPI schema with this kind of composition for the operations exercised. Requires a constructed fixture (a small mock OpenAPI spec with a `$ref`-based or `allOf`-composed response schema) to execute.

---

## Preconditions

- A toolkit built against a mock/fixture OpenAPI spec whose response schema for at least one operation uses `$ref` and at least one uses `allOf`/`anyOf`/`oneOf` composition to declare an array/collection field.

---

## Test Data

| Field | Value |
|-------|-------|
| Fixture spec | mock OpenAPI spec with `$ref`-based and composed response schemas (to be authored) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Build/import the fixture OpenAPI spec and configure a toolkit against it. | Toolkit configured successfully. |
| 2 | Call the `$ref`-based operation with `response_search`/`response_limit`. | The collection is correctly discovered and selected against — not silently skipped because of the `$ref` indirection. |
| 3 | Call the `allOf`/`anyOf`/`oneOf`-composed operation with `response_search`/`response_limit`. | Same correct discovery and selection behavior. |

---

## Expected Final State

Schema composition/indirection does not defeat collection discovery.

---

## Pass/Fail Criteria

**Pass:** Both composed-schema operations correctly discover and select their collections.
**Fail:** Either operation fails to discover the collection (falls through to ambiguous/not-found, or errors) due to the schema indirection.

---

## Blocked / Fixture Needed

This test case requires a constructed OpenAPI fixture spec (no public API tested this session exhibited the needed schema composition). Author a minimal fixture spec before executing.
