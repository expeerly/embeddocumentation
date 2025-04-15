# Expeerly Video Review Integration Guide

This guide explains how to integrate expeerly video reviews into your product pages. The integration enables both carousel-style video reviews and a detailed review block through a simple script integration. You can check this example integration [here](https://v0-expeerly-demo-shop-whqyon.vercel.app/).

**PLEASE NOTE: Using expeerly reviews as a retailer is free of charge**

Version 1.6, 16th of April 2025

## Table of Contents

- [Features](#features)
- [Integration Steps Expeerly for your Image Gallery/Carousel](#integration-steps-expeerly-for-your-image-gallerycarousel)
  - [Step 1: Get API acess](#step-1-get-api-acess)
  - [Step 2: Install Mux Player (Web, iOS, Android)](#step-2-install-mux-player-web-ios-android)
  - [Step 3: Call the expeerly API and pass your Store-ID](#step-3-call-the-expeerly-api-and-pass-your-store-id)
- [Integration Steps Expeerly Badge/Review Block Widget](#integration-steps-expeerly-badgereview-block-widget)
  - [Step 1: Get Your Integration Script](#step-1-get-your-integration-script)
  - [Step 2: Add the Script to the Head Section](#step-2-add-the-script-to-the-head-section)
  - [Step 3: Add the expeerly component to Your Product Pages](#step-3-add-the-expeerly-component-to-your-product-pages)
  - [Step 4: Pass your retailer tracking attribute](#step-4-pass-your-retailer-tracking-attribute)
  - [Customization](#customization)
  - [Testing your integration](#testing-your-integration)
  - [What the expeerly.js does](#what-the-expeerlyjs-does)
- [Optional: Check if reviews are available for given GTIN/EAN/UPC numbers](#optional-check-if-reviews-are-available-for-given-gtineanupc-numbers)


## Features

Our integration offers the possibiltiy to 
- **add video reviews directly to your image gallery** or carousel useing [mux](https://mux.com) as video streaming provider and 
- a **widget style implementation** for a badge and a review block that pulls data from the expeerly system and uses [mux](https://mux.com) as video streaming provider.

The integration provides:
- Video reviews in your product image carousel
- Detailed review block including:
  - Star ratings
  - Reviewer names and profile pictures
  - View counts (pending)
  - Expeerly branding
- Above-fold summary button linking to review block
- Zero-impact when no videos are available

## Integration Steps Expeerly for your Image Gallery/Carousel 

### Step 1: Get API acess

~Log into your Expeerly dashboard and copy the API token.~ PENDING 

For the beta phase, get in touch with the expeerly team directly at product@expeerly.com. The API is publicly available for now.

### Step 2: Install Mux Player (Web, iOS, Android)
Get the mux player that best fits your needs [here](https://www.mux.com/docs/guides/play-your-videos).

### Step 3: Call the expeerly API and pass your Store-ID
Call the expeerly API `https://app.expeerly.com/api/1.1/wf/get-product-videos-processed/?gtin=${GTIN/UPCnumber}`

The response is an array of videos. For setting up the mux player you will need the mux_playback_id_text

Example of returned Data:

```js
[
    {
      ...
      "mux_playback_id_text": "J9S1Qt6MKYxf01EgmAmyMyXpvFhb8g02p01301QhzUgptrM",
    },
]
```

Pass the `mux_playback_id_text` value to `playbackId`.

Note: Passing a StoreId value is important to help track the Views from your store.

To pass the StoreId of value `onlineshop1` on the mux tag like below.

HTML Example
```html
<mux-player
  metadata-custom-1={onlineshop1}
></mux-player>
```

React Example

```html
<MuxPlayer
  metadata={{
    'custom-1': 'onlineshop1',
  }}
></MuxPlayer>

```


## Integration Steps Expeerly Badge/Review Block Widget

### Step 1: Get Your Integration Script

~Log into your Expeerly dashboard and copy your unique integration script. This script is pre-configured with your shop's identifier and necessary credentials.~ PENDING 

For the beta phase, get in touch with the expeerly team directly at product@expeerly.com. The script is publicly available for now.

### Step 2: Add the Script to the Head Section
Add the following code snippet to your head section in your html code
```html
<script type="module" src="https://www.expeerly.com/expeerly.js"></script>
```

### Step 3: Add the expeerly component to Your Product Pages
Add the experly web component (with the gtin/ean/upc as an attribute) where ever you want to have experely videos shown:
```html
<expeerly-component gtin="123456789012"></expeerly-component>
```

### Step 4: Pass your retailer tracking attribute
In order to make sure that you, we and the brands can track where the view traffic is coming from, you need to pass the `store-id` attribute with your assigned value e.g:
```html
<expeerly-component gtin="123456789012" store-id="store1"></expeerly-component>
```

That's it! The Expeerly script will automatically:
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
| type | badge / reviewblock | select to show the data in the carousel, the button and/or as review block | reviewblock |
| theme | dark / light / miniminal | select the theme (background colour) | dark |
| max-videos | number | how many reviews should be loaded | undefined |
| locale | en / de / fr / it | for now we provide 4 languages, if there is no language we will use the html or browser defined language. If we don't provide the language we will use the default language  (if not set, it will use the global config settings) | en |
| store-id | string | What id would you want to track analytics on the video views? | undefined |

### Testing your integration
To test your integration you can call the following GTIN numbers: `4548736157088` Sony Ult Field 1, `7610045010440` Koenig Micro Wave, `8720689021937` Philips Baby Care Set or `4008789094636` Playmobil Fire Brigade Truck over the API.

### What the expeerly.js does
The script
- creates a video player from [mux](https://www.mux.com/) and streams the videos from the mux server.
- makes a request on the backend to get all important data for the reviews.
- registers a web component called expeerly-component

All styles are generated by the script and each class contains the prefix `expeerly`.

## Optional: Check if reviews are available for given GTIN/EAN/UPC numbers
If you would like to check which GTIN/EAN/UPC numbers have a review go to `expeerly.com/csv.html` [(click link here)](https://expeerly.com/csv.html) and get a list of product for which video reviews are available. The list is updated in real time and have a timestamp when you access it. This can be useful if you would like to avoid loading the expeerly integration on every page.
