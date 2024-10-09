# Embedding Expeerly Videos on Online Shops or Marketplaces: Developer Guide
This guide provides an overview of how to embed expeerly videos into your online shop or marketplace. It includes examples and step-by-step instructions to assist both product owners and developers in the integration process. Embedding via any of the solutions is free of charge for you as retail partner.

## 1. Options: Youtube or Mux
Expeerly offers 2 Video Embedding Solutions via [Youtube](https://www.youtube.com/) Embed Links or via [Mux](https://www.mux.com/).

## 2. Embedding with Youtube
### 2.1 Embedding a YouTube Video
To embed a YouTube video, use the iframe code.
```
<iframe width="560" height="315" src="https://www.youtube.com/embed/nqG3JCNkb0I?si=bikBYWxuWUS6SWCu" 
        title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; 
        encrypted-media; gyroscope; picture-in-picture; web-share" 
        referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
</iframe>
```
### 2.2 Embed examples
Galaxus shows the expeerly video in their image carousel, check this [link to the Philips Avent Kit](https://www.galaxus.ch/fr/s10/product/philips-avent-kit-de-soins-pour-bebe-soin-corporel-bebe-36358432?ip=8720689021937)

Brack shows the expeerly video in their image carousel, check this [link to the Philips Avent Kit ](https://www.brack.ch/philips-avent-baby-pflegeset-petrol-1614829)

But ultimately you're free to add the above embed code on any part of our online shop or marketplace. We recommend the carousel or product description just next to images for best conversion impact.

## 3. Embedding with Mux
### 3.1 Embedding with Mux Streaming Links
Mux Stream provides scalable video hosting, ideal for large volumes. You can use either the .mp4 format for static video playback or the .m3u8 format for adaptive streaming.

For on-demand playback: 
```
https://stream.mux.com/q2EyUPCM0000k3QbfjLVTmEL5N6PDL701aovfWx7QByv84/high.mp4
```

For adaptive streaming (ideal for varying bandwidths):
```
https://stream.mux.com/q2EyUPCM0000k3QbfjLVTmEL5N6PDL701aovfWx7QByv84.m3u8
```

### 3.2 Embed examples
#### MP4
Here is an example of a mux mp4 streaming link added to a website. It can be any website as all browsers are able to read mp4 formats and will trigger the native video controls.

Check our expeerly [corporate page](https://www.get.expeerly.com/) and scroll down to the Dyson customer quote. On this webflow we just add a play back [link](https://stream.mux.com/q2EyUPCM0000k3QbfjLVTmEL5N6PDL701aovfWx7QByv84/high.mp4) as above.

#### M3U8
For more freedom over video controls you can use the HLS (m3u8) URL in a player of your choice. See the documentation [here](https://docs.mux.com/guides/play-your-videos#3-use-the-hls-url-in-a-player).


### 3.3 Embedding with Mux Developer SDK
For a more customizable experience, use the Mux Developer SDK and add to your online shop or marketplace. You can find the documentation [here](https://docs.mux.com/guides/mux-player-web).

### 3.4 Embed example
Here is an example link for the Trisa Raclette Tischgrill video and how we integrate the Mux Web Player on our own expeerly.com video player page.
```
https://www.expeerly.com/de/video-reviews/elektronik-gadgets/trisa/raclette-tischgrill-style-connect/100000469
```

As you can see, [subtitles](https://docs.mux.com/guides/add-subtitles-to-your-videos#showing-subtitles-by-default) and separate [audio track](https://docs.mux.com/guides/player-core-functionality#multi-track-audio-selector) in 4 languages are available and can be triggered.

We recommend embedding the videos to the carousel or product description just next to images for best conversion impact.

## 4. Matching Video Links with Product Catalogue
As of now all our retail partners get a spreadsheet where on each line the relevant products including GTIN and if required our partner’s own product number are indicated along the video links. As our existing partners choose to embed with Youtube, it’s only Youtube links, but Mux links and Streaming IDs would be shown for your integration.

See an example [here](https://docs.google.com/spreadsheets/d/1kXQ7DBHRILnurgFzuOjY3owplIlcU94W2a_1l2gwAxg/edit?usp=sharing).

## 5. Choosing the Right Embedding Solution
### 5.1 Embedding solutions are free ofcharge 
No matter which solution you choose, for you as a retail partner they are **FREE OF CHARGE!**

### 5.2 Youtube
**Pros**
- Easy integration with a known technology
- Best for maximizing reach with public videos
  
**Cons**
- It **NEGATIVELY** impacts your conversion rate as you channel traffic out of your online shop to Youtube


### 5.3 Mux Streaming Links
**Pros**
- Easy integration with a simple streaming link
- Suited for high scalability with robust analytics and adaptive streaming
  
**Cons**
- Only native native video controls


### 5.4 Mux Embed SDK
**Pros**
- Customizable experience
- Suited for high scalability with robust analytics and adaptive streaming
  
**Cons**
- Needs most dev ressources

