---
id: ELITEA-0671
title: "Forked Pipeline Executes Successfully and Is Independent from Source Pipeline"
priority: high
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0671: Forked Pipeline Executes Successfully and Is Independent from Source Pipeline

**Module:** Fork · **Priority:** High · **Type:** Functional

**Objective:** Verify that a forked pipeline runs successfully in the target project and that its state variables are independent from the source pipeline.

**Coverage:**
- Post-fork pipeline executability
- Output correctness
- State variable isolation (changes in source do not affect fork)

## Preconditions

- Logged in as Editor in Source Project and Target Project
- Source Pipeline has a known, repeatable execution (simple deterministic pipeline)

## Test Data

- Pipeline test input: a simple text prompt or trigger value
- Expected output: known/recorded from source pipeline execution

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Source Project, run the pipeline with a test input → record the output | Output recorded |
| 2 | Fork the pipeline to Target Project | Fork completes |
| 3 | In Target Project → open the forked pipeline → execute with same test input | Pipeline runs |
| 4 | Verify execution completes without errors | No errors shown |
| 5 | Compare output to the recorded source output | Output matches |
| 6 | Modify a state variable default in the source pipeline and save | Source pipeline updated |
| 7 | Re-open the forked pipeline in Target Project | Forked pipeline open |
| 8 | Verify the forked pipeline state variable is unchanged by the source edit | State variable remains as set at fork time |

## Expected Final State

State variable remains as set at fork time

## Pass/Fail Criteria

**Pass:**
- Forked pipeline executes and produces expected output
- Source pipeline state change does not propagate to the forked pipeline

**Fail:**
- Forked pipeline fails to execute (error on run)
- Output differs from source in an unexpected way
- State variable in forked pipeline changes when source is edited
