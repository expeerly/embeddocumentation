# Brand Widget for Video Reviews – Integration Guide - PENDING

This guide explains how to integrate the **expeerly Brand Widget**, a lightweight JavaScript widget that automatically displays video reviews, aggregated ratings, and review counts across all products for a specific brand. It's built for easy, async integration into any website or online shop—just like a e.g live chat widget with optional styling.

**Version: 0.1**

**Publication pending**

---

## Table of Contents

- [Overview](#overview)
- [Integration Steps](#integration-steps)
  - [Step 1: Get Your Access Key and Brand ID](#step-1-get-your-access-key-and-brand-id)
  - [Step 2: Add the Script to Your Head Section](#step-2-add-the-script-to-your-head-section)
  - [Step 3 (Optional): Control Placement with Widget Tag](#step-3-optional-control-placement-with-widget-tag)
  - [Customization Options](#customization-options)
- [What the Widget Displays](#what-the-widget-displays)
- [Support](#support)


## Overview
The **expeerly Brand Widget** lets you embed a brand-level review summary on your site with a single script. By default, it appears on all pages, just like live chat or helpdesk widgets. 

The widget automatically:
- Queries Expeerly’s API for all product GTINs under a brand
- Aggregates ratings and reviews
- Shows all brand video reviews in an interactive fly-in player

### Mockup
- You can check a mockup of the widget design [here](https://drive.google.com/file/d/15zYmtFKxZgEnG4_TPtjwY8WKsGwzj8jz/view?usp=sharing).

### Key Features
- One-line integration
- Brand-level average rating and review count
- Video review fly-in player
- Appears automatically on every page
- Supports `light` and `dark` themes
- Fully async and non-blocking

## Integration Steps

### Step 1: Get Your Access Key and Brand ID

Request both from the Expeerly team at `product@expeerly.com`:

- Your **Access Key**
- Your **Brand ID**


### Step 2: Add the Script to Your Head Section

Insert the following snippet into the `<head>` of your website:

```html
<script type="module" async src="https://www.expeerly.com/expeerly.js"></script>
<script>
  const ExpeerlyFlyWidget = document.createElement('expeerly-fly-widget');
  ExpeerlyFlyWidget.setAttribute('access-key', 'abc123xyz');
      ExpeerlyFlyWidget.setAttribute('brand-id', 'yourBrand123');
      ExpeerlyFlyWidget.setAttribute('theme', 'light'); // or "dark"
      ExpeerlyFlyWidget.setAttribute('position', 'bottom-right'); // or "bottom-left", "top-left", "top-right"
      ExpeerlyFlyWidget.setAttribute('locale', 'de');
      document.body.appendChild(ExpeerlyFlyWidget);
</script>
```

This is all you need to get the widget live on all pages.


### Step 3 (Optional): Control Placement with Widget Tag

If you want to control where exactly the widget appears (e.g., inside a specific container), add the following tag to your HTML:

```html
<expeerly-fly-widget access-key="abc123xyz" brand-id="yourBrand123" theme="light" position="bottom-right" locale="de">
</expeerly-fly-widget>
```

If present, this overrides the default automatic placement.


## Customization Options

You can configure the widget using the available options. Below are the available options:

| Option       | Type   | Description                          | Values                | Default |
|--------------|--------|--------------------------------------|------------------------|---------|
| `brand-id`    | string | Required. Provided by Expeerly       | e.g. "brand123"        | —       |
| `access-key`  | string | Required. Provided by Expeerly       | e.g. "abc123xyz"       | —       |
| `theme`      | string | Choose widget theme                  | `light`, `dark`        | `light` |
| `locale`     | string | Interface language                   | `bottom-right`, `bottom-left`, `top-right`, `top-left` | top-right    |
| `position`     | string | Placement position for the flyin widget                   | `en`, `de`, `fr`, `it` | auto    |

Example:

```html
<script>
  const ExpeerlyFlyWidget = document.createElement('expeerly-fly-widget');
  ExpeerlyFlyWidget.setAttribute('access-key', 'abc123xyz');
      ExpeerlyFlyWidget.setAttribute('brand-id', 'yourBrand123');
      ExpeerlyFlyWidget.setAttribute('theme', 'light'); // or "dark"
      ExpeerlyFlyWidget.setAttribute('position', 'bottom-right'); // or "bottom-left", "top-left", "top-right"
      ExpeerlyFlyWidget.setAttribute('locale', 'de');
      document.body.appendChild(ExpeerlyFlyWidget);
</script>
```

## What the Widget Displays

Once loaded, the widget displays:

- Average Star Rating across for your brand based on all expeerly reviews
- Total Number of Reviews  
- All Video Reviews for the Brand in a fly-in slider  
- Automatically styled in light or dark theme  


---

## Support

For setup help, access credentials, or customization support, contact:  
**product@expeerly.com**
