
# Brand Widget for Video Reviews – Integration Guide

This guide explains how to integrate the **Expeerly Brand Widget**, a lightweight JavaScript widget that automatically displays video reviews, aggregated ratings, and review counts across all products for a specific brand. It's built for easy, async integration into any website or online shop—just like a live chat widget.

**Version:** 1.1  
**Date:** June 2025

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Integration Steps](#integration-steps)
  - [Step 1: Get Your Access Key and Brand ID](#step-1-get-your-access-key-and-brand-id)
  - [Step 2: Add the Script to Your Head Section](#step-2-add-the-script-to-your-head-section)
  - [Step 3 (Optional): Control Placement with Widget Tag](#step-3-optional-control-placement-with-widget-tag)
  - [Customization Options](#customization-options)
- [What the Widget Displays](#what-the-widget-displays)
- [Technical Notes](#technical-notes)
- [Support](#support)

---

## Overview

The **Expeerly Brand Widget** lets you embed a brand-level review summary on your site with a single script. By default, it appears on all pages, just like live chat or helpdesk widgets.

The widget automatically:

- Queries Expeerly’s API for all product GTINs under a brand
- Aggregates ratings and reviews
- Shows all brand video reviews in an interactive fly-in player

---

## Key Features

- One-line integration
- Brand-level average rating and review count
- Video review fly-in player
- Appears automatically on every page
- Supports `light` and `dark` themes
- Fully async and non-blocking

---

## How It Works

1. You include a script in your website’s `<head>`.
2. The widget loads asynchronously and appears automatically at the edge of every page.
3. Optionally, you can control placement with an HTML tag.
4. It pulls and displays brand-wide review data and videos using the brand ID.

---

## Integration Steps

### Step 1: Get Your Access Key and Brand ID

Request both from the Expeerly team at `product@expeerly.com`:

- Your **Access Key**
- Your **Brand ID**

---

### Step 2: Add the Script to Your Head Section

Insert the following snippet into the `<head>` of your website:

```html
<script type="module" async src="https://www.expeerly.com/brand-widget.js"></script>
<script>
  window.expeerlyBrand = {
    brandId: "yourBrand123",
    accessKey: "abc123xyz",
    theme: "light" // or "dark"
  };
</script>
