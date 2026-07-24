---
id: ELITEA-2315
title: "MDX with Unsafe JSX Components Shows Warning"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, feat:security, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2315: MDX with Unsafe JSX Components Shows Warning

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify MDX files with unsafe JSX components display warning banner and fallback to Markdown rendering

**Security Note:** This test verifies AC5 security requirements - unsafe JSX components must be blocked and warning displayed.

## Preconditions

- MDX file with JSX components exists in Artifacts

## Test Data

- File with JSX component: `<MyComponent>content</MyComponent>`
- Expected warning: "MDX compilation failed. Showing plain Markdown fallback."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or open MDX file with JSX component | File opens |
| 2 | Add JSX syntax: `<CustomButton>Click</CustomButton>` | Content added |
| 3 | Save the file | File saved |
| 4 | View in Preview mode | Preview displays |
| 5 | Observe warning banner at top | Warning banner visible |
| 6 | Observe content rendering | Markdown fallback shown |

## Expected Results

- Warning banner displays at top of Preview
- Warning text: "MDX compilation failed. Showing plain Markdown fallback."
- JSX components do not execute or render
- Markdown content still renders correctly
- File remains functional for Markdown content
- No JavaScript execution occurs
- Preview mode remains stable (no crashes)

## Pass/Fail Criteria

**Pass:**
- Warning banner appears with correct message
- JSX components are blocked from execution
- Markdown content renders in fallback mode
- No security vulnerabilities exploited

**Fail:**
- No warning displayed
- JSX components execute
- Content fails to render at all
- Security breach occurs
