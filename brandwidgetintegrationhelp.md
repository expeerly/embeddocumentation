# expeerly Brand Widget — Integration Help for Shop Systems

Below are two ready-to-implement paths to add the **[expeerly Brand Widget](https://github.com/expeerly/embeddocumentation/blob/main/brandwidgetvideoreviews.md)** to your store.

## Table of Contents
- [WordPress / WooCommerce (Custom Plugin)](#wordpress--woocommerce-custom-plugin)
 - [Install the plugin](#install-the-plugin)
 - [Configure the widget](#configure-the-widget)
 - [Optional: manual placement with shortcode](#optional-manual-placement-with-shortcode)
 - [Optional: disable global auto-load](#optional-disable-global-auto-load)
 - [Troubleshooting](#troubleshooting)
- [Shopify (Theme Integration)](#shopify-theme-integration)
 - [Option 1: Show on all pages (fastest)](#option-1-show-on-all-pages-fastest)
 - [Option 2: Products only](#option-2-products-only)
 - [Option 3: Show on specific pages only](#option-3-show-on-specific-pages-only)
 - [Notes & Best Practices (Shopify)](#notes--best-practices-shopify)
- [Credentials & Support](#credentials--support)

## WordPress / WooCommerce (Custom Plugin)

**Good to know:** You don't need to add any code. Just install our ZIP and configure it.

### 1) Install the plugin
1. Download the plugin [here](https://drive.google.com/drive/folders/1_Qk5DVe1C6taByCHigUFR_WXyvhDSa_D?usp=sharing).
2. Go to **WordPress Admin → Plugins → Add New → Upload Plugin**.
3. Upload the file **`expeerly-brand-widget.zip`** and click **Install Now**, then **Activate**.

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

The shortcode automatically uses your saved **Access Key** and **Brand ID**. Attributes are optional and override the saved display settings for that placement.

### 4) Optional: disable global auto-load
If you're using the shortcode, you can disable **Global auto-load** in the plugin settings to avoid duplicate widgets.

### 5) Troubleshooting
- **Nothing shows up:** Double-check **Access Key** and **Brand ID**.  
- **Double widget:** Disable **Global auto-load** if you also placed the shortcode.  
- **Caching/CDN:** Purge cache after first install or when changing settings.  
- **Theme conflicts:** Switch to shortcode placement to control the exact location.

---

## Shopify (Theme Integration)

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

