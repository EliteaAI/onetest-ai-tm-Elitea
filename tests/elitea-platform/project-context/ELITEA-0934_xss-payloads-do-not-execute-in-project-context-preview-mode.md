---
id: ELITEA-0934
title: "XSS Payloads Do Not Execute in Project Context Preview Mode"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, preview-mode, story:3395, security, r-2.0.4, xss]
requirements: [EliteaAI/elitea_issues#3395, EliteaAI/elitea_issues#5306]
---
# ELITEA-0934: XSS Payloads Do Not Execute in Project Context Preview Mode

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that XSS payloads embedded in Project Context content do not execute when switched to Preview mode.

**Coverage:**
- script tag not executed
- img onerror not triggered
- iframe not loaded
- CSS injection blocked
- javascript: protocol link blocked
- SVG onload not triggered

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

XSS payloads to include in content:
```html
<h2>7. SVG-based script execution test (must NOT execute)</h2>
  <svg>
    <script>
      console.log("FAIL: SVG SCRIPT EXECUTED");
    </script>
  </svg>
<script>alert('XSS via script tag')</script>
<img src=\"x\" onerror=\"alert('XSS via img onerror')\">
<iframe src=\"https://evil.example.com\" width=\"100%\" height=\"500\"></iframe>
<style>body { display: none !important; }</style>
<a href=\"javascript:alert('XSS via href')\">Click me</a>
<svg onload=\"alert('XSS via SVG onload')\"></svg>
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set the content to all XSS payloads from test data. Save. | Content saved without error. |
| 2 | Switch to Preview mode. | No alert() popup fires. Page remains stable. |
| 3 | Verify the script tag. | Script is not executed. Tag is shown as escaped text or removed entirely. |
| 4 | Verify the img onerror handler. | onerror does not fire. No alert. |
| 5 | Verify the iframe tag. | Iframe does not load the external URL. |
| 6 | Verify the style tag (body{display:none}). | Page UI is fully visible. CSS injection is blocked. |
| 7 | Click the javascript: protocol link. | No JavaScript executes on click. |

## Expected Final State

No JavaScript executes on click.

## Pass/Fail Criteria

**Pass:**
- No alert() or JS executes in Preview
- UI remains fully visible (no CSS hiding)
- No external content loaded

**Fail:**
- Any alert() popup fires
- UI elements hidden by injected CSS
- External URL loads in iframe
