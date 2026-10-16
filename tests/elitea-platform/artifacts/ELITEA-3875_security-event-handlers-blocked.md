---
id: ELITEA-3875
title: "Security - Event Handlers Blocked"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, feat:security, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3875: Security - Event Handlers Blocked

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify event handlers in JSX do not execute

**Security Note:** This validates AC5 security requirement - event handlers must not execute

## Preconditions

- MDX file contains JSX with event handlers: `<button onClick={() => alert('clicked')}>Click</button>`

## Test Data

- JSX with handler: `<button onClick={() => alert('clicked')}>Click</button>`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or locate MDX with event handler JSX | File ready |
| 2 | Open in Preview mode | Preview displays |
| 3 | Observe if button renders | Check rendering |
| 4 | Click on button (if visible) | Click action |
| 5 | Check browser console | Check console |
| 6 | Check for warning banner | Banner may display |

## Expected Results

- Event handlers do not execute
- JSX elements either render as static HTML without handlers (onClick stripped) OR display as code OR show warning banner: "MDX compilation failed. Showing plain Markdown fallback."
- No onClick/onLoad/onChange events fire
- Clicking button (if rendered) does nothing
- No alert appears
- Browser console shows no event execution
- Preview remains safe and sandboxed

## Pass/Fail Criteria

**Pass:**
- Event handlers do not execute
- No events fire
- Preview is safe

**Fail:**
- Event handlers execute
- Alert appears
- Security vulnerability
