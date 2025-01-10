# Expeerly Video Review Integration Guide

This guide explains how to integrate Expeerly video reviews into your product pages. The integration enables both carousel-style video reviews and a detailed review block through a simple script integration.

**PLEASE NOTE: Using expeerly reviews as a retailer is free of charge**

Version 1.2, 10th of January 2025

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

## Integration Steps

### Step 1: Get Your Integration Script

Log into your Expeerly dashboard and copy your unique integration script. This script is pre-configured with your shop's identifier and necessary credentials.

### Step 2: Add the Script to the Head Section
Add the following code snippet to your head section in your html code
```html
<script src="https://www.expeerly.com/embed.js"></script>
```

### Step 3: Add the Script to Your Product Pages

Add your unique integration script to your product page template just before the closing `</body>` tag:

```html
<!-- This is an example. Get your actual script from the Expeerly dashboard -->
<script>
    expeerly()
</script>
```

### Step 4: Add the Script to Your Product Pages
Add the experly HTML Tag(with the gtin as an attribute) where ever you want to have experely videos shown:
```html
<expeerly gtin="123456789012"></expeerly>
```

That's it! The Expeerly script will automatically:
- Check for available video reviews
- Add videos to your product carousel if available
- Create a review block with detailed information
- Add a summary button above the fold
- Handle all analytics tracking

## Customization

To globally customize the appearance of the Expeerly integration, you can add optional data attributes to your script tag:

```html
<script>
    expeerly({accentColor: "#2C1277", locale: "en"})
</script>
```

To customize individual integrations you can add attributes to the expeerly HTML Tag:

```html
<expeerly data-videoonly="true" data-theme="dark" data-max="12"></expeerly>
```

Available data attributes:
| Name | Type | Description | Default |
| -------- | ------- | -------- | ------- |
| videoonly | true / false | wether to show the data as carousel or as videos | false |
| theme | dark / light | what them should be used | light |
| max | number | how many reviews should be loaded | undefined |

## What the embed.js does
```
const expeerly = (function() {
  // Configuration 
  const BUBBLE_API = 'https://appname.bubbleapps.io/api/1.1/obj/videos';
  const DEFAULT_OPTIONS = {
    display: 'both',
    accentColor: '#2C1277',
    language: 'en'
  };

  // Helper to create elements with classes
  const createElement = (tag, className = '') => {
    const element = document.createElement(tag);
    if (className) element.className = className;
    return element;
  };

  // Get data attributes from script tag
  const getScriptOptions = () => {
    const script = document.currentScript;
    return {
      gtin: script.dataset.gtin,
      display: script.dataset.display || DEFAULT_OPTIONS.display,
      accentColor: script.dataset.accentColor || DEFAULT_OPTIONS.accentColor,
      language: script.dataset.language || DEFAULT_OPTIONS.language
    };
  };

  // Create summary button
  const createSummaryButton = (rating, reviewCount) => {
    const button = createElement('button', 'expeerly-summary-btn');
    button.innerHTML = `
      <img src="https://expeerly.com/logo.svg" alt="Expeerly" class="expeerly-logo">
      <span>${rating.toFixed(1)} ★ (${reviewCount} reviews)</span>
    `;
    button.onclick = () => {
      document.querySelector('.expeerly-review-block').scrollIntoView({ behavior: 'smooth' });
    };
    return button;
  };

  // Create carousel item
  const createCarouselItem = (video) => {
    const container = createElement('div', 'expeerly-carousel-item');
    container.innerHTML = `
      <mux-player
        playback-id="${video.playbackId}"
        metadata-video-title="${video.videoTitle}"
        metadata-custom-1="${video.shopId}"
        stream-type="on-demand"
        prefer-playback="mse"
        style="width: 100%; aspect-ratio: 9/16;">
      </mux-player>
    `;
    return container;
  };

  // Create review block item
  const createReviewBlockItem = (video) => {
    const container = createElement('div', 'expeerly-review-item');
    container.innerHTML = `
      <div class="expeerly-review-header">
        <img src="${video.profilePicture}" alt="${video.reviewerName}" class="expeerly-reviewer-pic">
        <div class="expeerly-reviewer-info">
          <div class="expeerly-reviewer-name">${video.reviewerName}</div>
          <div class="expeerly-rating">${'★'.repeat(Math.floor(video.rating))}${'☆'.repeat(5 - Math.floor(video.rating))}</div>
        </div>
        <div class="expeerly-views">${video.viewCount} views</div>
      </div>
      <mux-player
        playback-id="${video.playbackId}"
        metadata-video-title="${video.videoTitle}"
        metadata-custom-1="${video.shopId}"
        stream-type="on-demand"
        prefer-playback="mse"
        style="width: 100%; aspect-ratio: 9/16;">
      </mux-player>
      <div class="expeerly-info">
        Expeerly is an independent review community and service. <a href="https://expeerly.com" target="_blank">Learn more</a>.
      </div>
    `;
    return container;
  };

  // Main initialization function
  const init = async () => {
    const options = getScriptOptions();
    
    try {
      // Fetch videos from Bubble API
      const response = await fetch(`${BUBBLE_API}?gtin=${options.gtin}`);
      const data = await response.json();
      
      if (!data.results || data.results.length === 0) {
        return; // No videos available
      }

      const videos = data.results;
      const averageRating = videos.reduce((acc, v) => acc + v.rating, 0) / videos.length;

      // Create and insert summary button
      const summaryButton = createSummaryButton(averageRating, videos.length);
      document.body.appendChild(summaryButton);

      // Handle carousel integration if enabled
      if (options.display === 'carousel' || options.display === 'both') {
        const productCarousel = document.querySelector('[data-product-carousel]');
        if (productCarousel) {
          videos.forEach(video => {
            productCarousel.appendChild(createCarouselItem(video));
          });
        }
      }

      // Handle review block if enabled
      if (options.display === 'block' || options.display === 'both') {
        const reviewBlock = createElement('div', 'expeerly-review-block');
        videos.forEach(video => {
          reviewBlock.appendChild(createReviewBlockItem(video));
        });
        document.body.appendChild(reviewBlock);
      }

    } catch (error) {
      console.error('Expeerly initialization error:', error);
    }
  };

  // Add styles
  const styles = document.createElement('style');
  styles.textContent = `
    .expeerly-summary-btn {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      border-radius: 8px;
      background: #2C1277;
      cursor: pointer;
      transition: all 0.2s;
    }

    .expeerly-logo {
      height: 24px;
    }

    .expeerly-review-block {
      display: flex;
      flex-direction: column;
      gap: 24px;
      padding: 24px;
      max-width: 768px;
      margin: 0 auto;
    }

    .expeerly-review-item {
      border: 1px solid #2C1277;
      border-radius: 12px;
      overflow: hidden;
    }

    .expeerly-review-header {
      display: flex;
      align-items: center;
      padding: 12px;
      gap: 12px;
    }

    .expeerly-reviewer-pic {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      object-fit: cover;
    }

    .expeerly-reviewer-info {
      flex: 1;
    }

    .expeerly-rating {
      color: #FFC122;
    }

    .expeerly-views {
      color: white;
      font-size: 14px;
    }

    .expeerly-carousel-item {
      width: 100%;
      aspect-ratio: 9/16;
    }

    .expeerly-info {
      margin-top: 12px;
      padding: 0 12px 12px;
      font-size: 14px;
      color: #6b7280;
    }

    .expeerly-info a {
      color: #2C1277;
      text-decoration: underline;
    }
  `;
  document.head.appendChild(styles);

  // Initialize when DOM is ready
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
  } else {
    init();
  }
})();
```
