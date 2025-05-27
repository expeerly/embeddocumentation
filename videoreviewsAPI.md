# Expeerly Video Review Integration Guide

This guide explains how to integrate expeerly video reviews into your product pages. The integration enables both adding videos to your image gallery/carousel and a detailed review block through a simple script integration. You can check this example integration [here](https://v0-expeerly-demo-shop.vercel.app/).

**PLEASE NOTE: Using expeerly reviews as a retailer is free of charge**

Version 1.8, 27th of April 2025

## Table of Contents

## Table of Contents
- [Features](#features)
- [Integration Steps Expeerly for your Image Gallery/Carousel](#integration-steps-expeerly-for-your-image-gallerycarousel)
  - [Step 1: Get Your Access Key](#step-1-get-your-access-key)
  - [Step 2: Install Mux Player (Web, iOS, Android)](#step-2-install-mux-player-web-ios-android)
  - [Step 3: Prefetch and store available reviews](#step-3-prefetch-and-store-available-reviews)
  - [Step 4: Call the expeerly API and pass your Store-ID for tracking](#step-4-call-the-expeerly-api-and-pass-your-store-id-for-tracking)
    - [API call](#api-call)
    - [Store ID for Tracking](#store-id-for-tracking)
- [Integration Steps Expeerly Badge/Review Block Widget](#integration-steps-expeerly-badgereview-block-widget)
  - [Step 1: Get Your Access Key](#step-1-get-your-access-key-1)
  - [Step 2: Add the expeerly Script to the Head Section](#step-2-add-the-expeerly-script-to-the-head-section)
  - [Step 3: Add the expeerly component to Your Product Pages](#step-3-add-the-expeerly-component-to-your-product-pages)
  - [Step 4: Prefetch and store available reviews](#step-4-prefetch-and-store-available-reviews)
  - [Step 5: Pass your Store-ID for Tracking](#step-5-pass-your-store-id-for-tracking)
  - [Customization](#customization)
  - [Testing your Integration](#testing-your-integration)
  - [What the expeerly.js does](#what-the-expeerlyjs-does)


## Features

Our integration offers the possibiltiy to

- **add video reviews directly to your image gallery** or carousel using [mux](https://mux.com) as video streaming provider and
- a **widget style implementation** for a badge and a review block that pulls data from the expeerly system and uses [mux](https://mux.com) for videos.

The integration provides:

- Video reviews in your product image gallery/carousel
- Detailed review block including:
  - Star ratings
  - Reviewer names and profile pictures
  - View counts (pending)
  - Expeerly branding
- Above-fold summary button linking to review block
- Zero-impact when no videos are available

## Integration Steps Expeerly for your Image Gallery/Carousel

### Step 1: Get Your Access Key

To get your Access Key, please contact the expeerly team directly at <product@expeerly.com>. They will provide your store Access Key.

Pass the provided Access Key in the expeerly API.

### Step 2: Install Mux Player (Web, iOS, Android)

Get the mux player that best fits your needs [here](https://www.mux.com/docs/guides/play-your-videos).

**PLEASE NOTE: The use of the Mux Player is mandatory if you want to integrate expeerly video reviews in your product image gallery/carousel.**

### Step 3: Prefetch and store available reviews

Check which GTIN/EAN/UPC numbers have a review go to `expeerly.com/csv.html` [(click link here)](https://expeerly.com/csv.html) and get a list of products for which video reviews are available. The list is updated in real time and have a timestamp when you access it. It provides a main GTIN/EAN and UPC number as well as all size and colour variants of the same product.

### Step 4: Call the expeerly API and pass your Store-ID for tracking

#### API call

Call the expeerly API `https://api.expeerly.com/api/videos?access_key=${accesskey}&gtin=${GTIN/UPCnumber}`

Example of API call:
```
https://api.expeerly.com/api/videos?access_key=h233i2q1l23w837w1k29we4mn8ui03gh&gtin=123456789012
```

The response is an array of videos. For setting up the mux player you will need the mux_playback_id_text

Example of returned data:

```js
[
    {
      ...
      "muxPlaybackId": "J9S1Qt6MKYxf01EgmAmyMyXpvFhb8g02p01301QhzUgptrM",
    },
]
```

Pass the `muxPlaybackId` value to `playbackId`.

#### Store ID for Tracking

**Please note:** In order to make sure that you, we and the brands can track where the view traffic is coming from, passing a StoreId value is mandatory to track the views from your store. Please use the ID provided by the expeerly product team.

To pass the StoreId of value `store1` on the mux tag check the examples below.

HTML Example

```html
<mux-player
  metadata-custom-1={store1}
></mux-player>
```

React Example

```html
<MuxPlayer
  metadata={{
    'custom-1': 'store1',
  }}
></MuxPlayer>

```

## Integration Steps Expeerly Badge/Review Block Widget

### Step 1: Get Your Access Key

To get Access Key, please contact the expeerly team directly at <product@expeerly.com>. They will provide your store Access Key.

Pass the provided Access Key as attribue.

### Step 2: Add the expeerly Script to the Head Section

Add the following code snippet to your head section in your html code

```html
<script type="module" src="https://www.expeerly.com/expeerly.js"></script>
```

### Step 3: Add the expeerly component to Your Product Pages

Add the experly web component (with the gtin/ean/upc and access-key as an attribute) where ever you want to have experely videos shown:

```html
<expeerly-component gtin="123456789012" access-key="h233i2q1l23w837w1k29we4mn8ui03gh"></expeerly-component>
```

### Step 4: Prefetch and store available reviews
Check which GTIN/EAN/UPC numbers have a review go to `expeerly.com/csv.html` [(click link here)](https://expeerly.com/csv.html) and get a list of products for which video reviews are available. The list is updated in real time and have a timestamp when you access it. It provides a main GTIN/EAN and UPC number as well as all size and colour variants of the same product. 

### Step 5: Pass your Store-ID for Tracking

In order to make sure that you, we and the brands can track where the view traffic is coming from, passing a StoreId value is mandatory to track the views from your store. Please use the ID provided by the expeerly product team. e.g:

```html
<expeerly-component gtin="123456789012" access-key="h233i2q1l23w837w1k29we4mn8ui03gh" store-id="store1"></expeerly-component>
```

That's it! The expeerly script will automatically:

- Check for available video reviews
- Add videos to your product carousel if available
- Create a review block with detailed information
- Add a summary button above the fold
- Handle all analytics tracking

### Customization

To globaly customize the appearance of the Expeerly integration, you can overwrite the config stored in the window object:

```html
<script>
    window.expeerly.config.accentColor = "#2C1277"
    window.expeerly.config.locale = "en"
</script>
```

Available configurations:

| Name | Type | Description | Default |
| :--- | :--- | :---- | :--- |
| accentColor | any color like hex / rgba / hsl | set the accent color for the main color | undefined |
| locale | en / de / fr / it | for now we provide 4 languages, if there is no language we will use the html or browser defined language. If we don't provide the language we will use the default language | en |

To customize individual integrations you can add attributes to the expeerly html element:

```html
<expeerly-component type="badge" theme="dark" max-videos="12"></expeerly-component>
```

Available data attributes:

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| type | badge / reviewblock | select to show the data in the button or as review block | reviewblock |
| theme | dark / light / miniminal | select the theme (background colour) | dark |
| access-key | string | access key given to you by expeerly team | undefined |
| max-videos | number | how many reviews should be loaded | undefined |
| locale | en / de / fr / it | for now we provide 4 languages, if there is no language we will use the html or browser defined language. If we don't provide the language we will use the default language  (if not set, it will use the global config settings) | en |
| store-id | string | What id would you want to track analytics on the video views? | undefined |

### Testing your Integration

To test your integration you can call the following GTIN numbers: `4548736157088` Sony Ult Field 1, `7610045010440` Koenig Micro Wave, `8720689021937` Philips Baby Care Set or `4008789094636` Playmobil Fire Brigade Truck over the API.

### What the expeerly.js does

The script

- creates a video player from [mux](https://www.mux.com/) and streams the videos from the mux server,
- makes a request on the backend to get all important data for the reviews,
- registers a web component called expeerly-component.

All styles are generated by the script and each class contains the prefix `expeerly`.
