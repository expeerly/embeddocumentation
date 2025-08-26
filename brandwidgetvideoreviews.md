# Brand Widget for Video Reviews – Integration Guide - BETA

This guide explains how to integrate the **expeerly Brand Widget**, a lightweight JavaScript widget that automatically displays video reviews, aggregated ratings, and review counts across all products for a specific brand. It's built for easy, async integration into any website or online shop—just like a e.g live chat widget with optional styling.

**Version: 1.0, 25.08.2025**

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
| `position`     | string | Placement position for the flyin widget                   | `bottom-right`, `bottom-left`, `top-right`, `top-left` | top-right    |
| `locale`     | string | Interface language                   | `en`, `de`, `fr`, `it` |  auto    |

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
# expeerly Brand Widget — Integration Help (WordPress/WooCommerce & Shopify)

Below are two ready-to-implement paths to add the **expeerly Brand Widget** to your store. Both follow your BETA guide (v1.0, 25.08.2025) and keep the widget async and non-blocking.

---

## Part A — WordPress / WooCommerce (Custom Plugin)

> **Good to know:** You don't need to add any code. Just install our ZIP and configure it.

### 1) Install the plugin
1. Go to **WordPress Admin → Plugins → Add New → Upload Plugin**.
2. Upload the file **`expeerly-brand-widget.zip`** and click **Install Now**, then **Activate**.

### 2) Configure the widget
1. Go to **Settings → expeerly Brand Widget**.
2. Enter your **Access Key** and **Brand ID** (provided by expeerly).
3. Optional display settings:
   - **Theme:** `light` or `dark`
   - **Position:** `bottom-right`, `bottom-left`, `top-right`, `top-left`
   - **Locale:** `auto`, `en`, `de`, `fr`, `it`
   - **Where to show:**  
     - **All pages** (default)  
     - **WooCommerce product pages only**  
     - **Selected post types** (Pages, Posts, Products)

### 3) Optional: manual placement with shortcode
If you prefer to place the widget in a specific spot (e.g., inside your product description), add this shortcode where you want it to appear:

```
[expeerly_fly_widget theme="light" position="bottom-right" locale="auto"]
```

> The shortcode automatically uses your saved **Access Key** and **Brand ID**. Attributes are optional and override the saved display settings for that placement.

### 4) Optional: disable global auto-load
If you're using the shortcode, you can disable **Global auto-load** in the plugin settings to avoid duplicate widgets.

### 5) Troubleshooting
- **Nothing shows up:** Double-check **Access Key** and **Brand ID**.  
- **Double widget:** Disable **Global auto-load** if you also placed the shortcode.  
- **Caching/CDN:** Purge cache after first install or when changing settings.  
- **Theme conflicts:** Switch to shortcode placement to control the exact location.

---

## Part B — Shopify (Theme Integration)

You'll add a small snippet and decide where it should render (all pages, products only, or selected templates).

### Option 1: Show on all pages (fastest)
1. Shopify Admin → **Online Store → Themes → … → Edit code**.
2. Open **`layout/theme.liquid`** (or your main layout file).
3. **Before** the closing `</head>`, add the expeerly loader script:

```liquid
<script type="module" async src="https://www.expeerly.com/expeerly.js"></script>
```

4. **Before** the closing `</body>`, initialize the widget:

```liquid
<script>
  document.addEventListener('DOMContentLoaded', function() {
    var el = document.createElement('expeerly-fly-widget');
    el.setAttribute('access-key', '{{ settings.expeerly_access_key | default: "YOUR_ACCESS_KEY" }}');
    el.setAttribute('brand-id', '{{ settings.expeerly_brand_id | default: "YOUR_BRAND_ID" }}');
    el.setAttribute('theme', 'light'); // light | dark
    el.setAttribute('position', 'bottom-right'); // bottom-right | bottom-left | top-right | top-left

    // Try to map Shopify locale to expeerly locale
    {% assign iso = request.locale.iso_code | downcase %}
    {% if iso contains 'de' %} el.setAttribute('locale', 'de');
    {% elsif iso contains 'fr' %} el.setAttribute('locale', 'fr');
    {% elsif iso contains 'it' %} el.setAttribute('locale', 'it');
    {% else %} el.setAttribute('locale', 'en'); {% endif %}

    document.body.appendChild(el);
  });
</script>
```

**Tip:** For ease of maintenance, add theme settings for `expeerly_access_key` and `expeerly_brand_id` in your theme's `settings_schema.json`. Until then, replace the default placeholders above with your live values.

### Option 2: Products only
Add the loader once globally, then initialize only on product templates.

1. Add the loader in `layout/theme.liquid` (once, before `</head>`):

```liquid
<script type="module" async src="https://www.expeerly.com/expeerly.js"></script>
```

2. Initialize in your product template (e.g., `templates/product.liquid` or a product section like `sections/main-product.liquid`), near the end of the file:

```liquid
{% if template.name == 'product' %}
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      var el = document.createElement('expeerly-fly-widget');
      el.setAttribute('access-key', '{{ settings.expeerly_access_key | default: "YOUR_ACCESS_KEY" }}');
      el.setAttribute('brand-id', '{{ settings.expeerly_brand_id | default: "YOUR_BRAND_ID" }}');
      el.setAttribute('theme', 'light');
      el.setAttribute('position', 'bottom-right');

      {% assign iso = request.locale.iso_code | downcase %}
      {% if iso contains 'de' %} el.setAttribute('locale', 'de');
      {% elsif iso contains 'fr' %} el.setAttribute('locale', 'fr');
      {% elsif iso contains 'it' %} el.setAttribute('locale', 'it');
      {% else %} el.setAttribute('locale', 'en'); {% endif %}

      document.body.appendChild(el);
    });
  </script>
{% endif %}
```

### Option 3: Show on specific pages only
For example, homepage + selected collections, but not elsewhere.

1. Loader in `layout/theme.liquid` (once, before `</head>`):

```liquid
<script type="module" async src="https://www.expeerly.com/expeerly.js"></script>
```

2. Initialize conditionally near `</body>` in `layout/theme.liquid`:

```liquid
{% assign should_show_expeerly = false %}

{%- comment -%} Examples — choose the conditions you want {%- endcomment -%}
{% if template.name == 'index' %}
  {% assign should_show_expeerly = true %}
{% endif %}

{% if template.name == 'collection' and collection.handle == 'new-arrivals' %}
  {% assign should_show_expeerly = true %}
{% endif %}

{%- comment -%} Or limit to products from a specific vendor (brand) {%- endcomment -%}
{% if template.name == 'product' and product.vendor == 'Your Vendor Name' %}
  {% assign should_show_expeerly = true %}
{% endif %}

{% if should_show_expeerly %}
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      var el = document.createElement('expeerly-fly-widget');
      el.setAttribute('access-key', '{{ settings.expeerly_access_key | default: "YOUR_ACCESS_KEY" }}');
      el.setAttribute('brand-id', '{{ settings.expeerly_brand_id | default: "YOUR_BRAND_ID" }}');
      el.setAttribute('theme', 'light');
      el.setAttribute('position', 'bottom-right');

      {% assign iso = request.locale.iso_code | downcase %}
      {% if iso contains 'de' %} el.setAttribute('locale', 'de');
      {% elsif iso contains 'fr' %} el.setAttribute('locale', 'fr');
      {% elsif iso contains 'it' %} el.setAttribute('locale', 'it');
      {% else %} el.setAttribute('locale', 'en'); {% endif %}

      document.body.appendChild(el);
    });
  </script>
{% endif %}
```

### Notes & Best Practices (Shopify)
- **Don't duplicate initialization.** Load the script once; initialize only where needed.
- **Locales:** We auto-map Shopify's locale to en/de/fr/it. Override by setting a fixed value if desired.
- **Performance:** The widget loads async and is non-blocking.
- **Consent (GDPR):** If you use a consent app, wrap the initialization in your consent callback.
- **Hydrogen/Headless:** Inject the same script and init block in your app's root layout or the product route component.

---

## Credentials & Support

You will receive your **Access Key** and **Brand ID** from product@expeerly.com.

For assistance, email product@expeerly.com with:
- Your store URL
- Theme name/version (Shopify) or site URL (WordPress)
- Where you want the widget to appear (all pages, product only, specific templates)
