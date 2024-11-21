# Middleware-based Expeerly Video Review Integration

This solution outlines a middleware-based architecture for embedding Expeerly video reviews into retailer websites. It leverages GTIN/EAN codes for matching product metadata, ensuring secure and standardized data delivery via a hosted middleware service.

---

## Architecture Overview

### Components:
1. **Bubble API**: Source of video metadata, ratings, and reviewer details.
2. **Middleware Service**:
   - Built with **Next.js**.
   - Acts as an intermediary for secure and efficient communication.
   - Matches GTIN/EAN codes to video metadata and returns structured data.
3. **Retailer JavaScript Snippet**:
   - Fetches data via the middleware API.
   - Dynamically renders Mux Player, ratings, and reviewer details.

### Data Flow:
1. Retailer script sends a request to the middleware with the GTIN/EAN code.
2. Middleware queries the Bubble API for corresponding data.
3. Middleware returns structured metadata to the script.
4. Retailer script dynamically renders the content.

---

## Middleware Implementation

### Next.js API Route
Middleware service handles GTIN/EAN lookup and returns transformed data.

**`/pages/api/video-data.js`**
```javascript
import axios from "axios";

export default async function handler(req, res) {
  const { gtin } = req.query;

  if (!gtin) {
    return res.status(400).json({ error: "GTIN is required" });
  }

  try {
    const bubbleResponse = await axios.get(
      `https://appname.bubbleapps.io/api/1.1/obj/videos?constraints=[{"key":"gtin","constraint_type":"equals","value":"${gtin}"}]`,
      {
        headers: { Authorization: `Bearer YOUR_BUBBLE_API_KEY` },
      }
    );

    const data = bubbleResponse.data?.results[0];
    if (!data) {
      return res.status(404).json({ error: "No video data found for GTIN" });
    }

    const transformedData = {
      playbackId: data.playback_id,
      videoTitle: data.video_title,
      reviewerName: data.reviewer_name,
      location: data.location,
      rating: data.rating,
      reviewText: data.review_text,
      gtin: data.gtin,
    };

    res.status(200).json(transformedData);
  } catch (error) {
    console.error("Middleware error:", error);
    res.status(500).json({ error: "Internal Server Error" });
  }
}
```
## Retailer JavaScript Snippet
Retailers embed the following script in their product pages:

### Snippet Example
```html
<script>
  (function (d, s, gtin, options) {
    const script = d.createElement("script");
    script.src = "https://yourdomain.com/embed.js";
    script.onload = function () {
      ExpeerlyEmbed.init(gtin, options);
    };
    d.head.appendChild(script);
  })(document, "script", "1234567890123", {
    accentColor: "#ff5733", // Optional custom styling
    containerId: "expeerly-video-container", // ID of the container div
  });
</script>
<div id="expeerly-video-container"></div>
```

## Hosted Embed Script (embed.js)

The hosted script fetches metadata from the middleware and dynamically renders the video player and reviewer details.

### Script Example
```javascript
const ExpeerlyEmbed = (() => {
  async function fetchVideoData(gtin) {
    const response = await fetch(`https://yourdomain.com/api/video-data?gtin=${gtin}`);
    if (!response.ok) throw new Error("Failed to fetch video data");
    return response.json();
  }

  function renderStars(rating) {
    const fullStar = "⭐";
    const emptyStar = "☆";
    return fullStar.repeat(Math.floor(rating)) + emptyStar.repeat(5 - Math.floor(rating));
  }

  function renderContent(data, options) {
    const container = document.getElementById(options.containerId || "expeerly-video-container");
    if (!container) throw new Error("Container not found");

    container.innerHTML = `
      <div style="max-width: 640px; margin: 20px auto; font-family: Arial, sans-serif; text-align: left;">
        <mux-player
          playback-id="${data.playbackId}"
          metadata-video-title="${data.videoTitle}"
          style="width: 100%; border-radius: 8px;"
          accent-color="${options.accentColor || "#ea580c"}">
        </mux-player>
        <div style="margin-top: 10px; display: flex; align-items: center;">
          <img src="https://via.placeholder.com/50" alt="${data.reviewerName}" style="border-radius: 50%; width: 50px; height: 50px; margin-right: 10px;">
          <div>
            <p><strong>${data.reviewerName}</strong> from ${data.location}</p>
            <p style="color: gold;">${renderStars(data.rating)} (${data.rating} / 5)</p>
          </div>
        </div>
        <div style="text-align: center; margin-top: 10px;">
          <img src="https://example.com/expeerly-logo.png" alt="Expeerly Logo" style="width: 100px;">
        </div>
      </div>
    `;
  }

  return {
    async init(gtin, options = {}) {
      try {
        const data = await fetchVideoData(gtin);
        renderContent(data, options);
      } catch (error) {
        console.error("Expeerly Embed Error:", error);
      }
    },
  };
})();


## Customization Options

Retailers can customize the embed by passing options:

- **accentColor**: Adjust the Mux Player theme color.
- **containerId**: Specify the container where the content is rendered.

---

### API Response Example

Middleware returns standardized JSON:

```json
{
  "playbackId": "EcHgOK9coz5K4rjSwOkoE7Y7O01201YMIC200RI6lNxnhs",
  "videoTitle": "Expeerly Review for Product XYZ",
  "reviewerName": "John",
  "location": "Zurich, Switzerland",
  "rating": 4.5,
  "reviewText": "Great product, highly recommended!",
  "gtin": "1234567890123"
}

