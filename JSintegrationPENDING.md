# Expeerly Video Review Integration Guide

This guide explains how to integrate Expeerly video reviews into your product pages. The integration enables both carousel-style video reviews and a detailed review block through a simple script integration.

## Integration Steps

### Step 1: Install Mux Player

Add the Mux Player SDK to your website's `<head>` section. This is required to play the video reviews:

```html
<script src="https://unpkg.com/@mux/mux-player"></script>
```

### Step 2: Get Your Integration Script

Log into your Expeerly dashboard and copy your unique integration script. This script is pre-configured with your shop's identifier and necessary credentials.

### Step 3: Add the Script to Your Product Pages

Add your unique integration script to your product page template just before the closing `</body>` tag:

```html
<!-- This is an example. Get your actual script from the Expeerly dashboard -->
<script>
  !function(w,d,g){var s=d.createElement('script');s.src='https://expeerly.com/embed.js';s.async=true;s.dataset.gtin=g;d.body.appendChild(s)}(window,document,'YOUR_PRODUCT_GTIN');
</script>
```

That's it! The Expeerly script will automatically:
- Check for available video reviews
- Add videos to your product carousel if available
- Create a review block with detailed information
- Add a summary button above the fold
- Handle all analytics tracking

## Features

The integration automatically provides:
- Video reviews in your product image carousel
- Detailed review block including:
  - Star ratings
  - Reviewer names and profile pictures
  - View counts
  - Expeerly branding
- Above-fold summary button linking to review block
- Zero-impact when no videos are available

## Customization

To customize the appearance of the Expeerly integration, you can add optional data attributes to your script tag:

```html
<script 
  src="https://expeerly.com/embed.js" 
  data-gtin="YOUR_PRODUCT_GTIN"
  data-accent-color="#FF5733"
  data-language="en"
  data-display="both"
  async>
</script>
```

Available data attributes:
- `data-display`: Control display mode ('carousel', 'block', or 'both')
- `data-accent-color`: Customize the brand color
- `data-language`: Set the interface language
