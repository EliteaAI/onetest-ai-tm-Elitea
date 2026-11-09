---
id: ELITEA-9999
title: "Verify build-index workflow PR+merge path"
priority: low
type: functional
module: ci/verification
status: draft
execution_type: manual
tags: [ci-verification]
requirements: []
automation_test_id: []
---
# ELITEA-9999: Verify build-index workflow PR+merge path

Throwaway case used to exercise the `build-index` GitHub Actions workflow's
new push → PR → squash-merge path after the `main` branch-protection ruleset
started requiring PRs. Safe to delete once confirmed working.
