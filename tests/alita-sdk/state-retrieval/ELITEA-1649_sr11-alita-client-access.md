---
id: ELITEA-1649
title: "SR11 - alita_client Access"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, runtime_context, alita_client, code_node]
requirements: []
---
# ELITEA-1649: SR11 - alita_client Access

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify that alita_client is accessible from code nodes and exposes expected methods such as unsecret and get_prompt for runtime platform operations.

## Preconditions

Pipeline engine is running and accessible
Alita platform client is configured and injected into code node execution context
No LLM node required (code node only)
Test pipeline: suites/state_retrieval/tests/test_case_11_alita_client_access.yaml

## Test Data

secret_name: "test_secret_name"
Entry point: test_client_access (code node)
Runtime context: alita_client must be injected into code execution environment by pipeline engine

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize state with secret_name='test_secret_name' | State set with secret_name variable |
| 2 | Execute code node 'test_client_access'; code checks 'alita_client' in dir() or globals() | client_available=True; alita_client is present in the code execution context |
| 3 | Code inspects alita_client: retrieves type name, checks hasattr(alita_client, 'unsecret'), hasattr(alita_client, 'get_prompt') | has_unsecret_method=True, has_get_prompt_method=True; alita_client is not None |
| 4 | Code attempts to call alita_client.unsecret(secret_name='nonexistent_test_secret') | unsecret_callable=True; method is callable without raising an exception (returns None for non-existent secret) |
| 5 | Code reads secret_name from alita_state and verifies it equals 'test_secret_name' | secret_name_correct=True; state access works correctly alongside alita_client access |
| 6 | Verify test_results.test_passed from code node | test_results.test_passed=True; client_available=True, has_unsecret_method=True, secret_name_correct=True |

## Expected Final State

test_results.test_passed=True; client_available=True, has_unsecret_method=True, secret_name_correct=True

## Pass/Fail Criteria

PASS: test_passed=True, client_available=True, has_unsecret_method=True, secret_name_correct=True
FAIL: alita_client not found in code execution context (not injected by pipeline engine)
FAIL: alita_client does not have 'unsecret' or 'get_prompt' methods
FAIL: Calling unsecret() raises unhandled exception
