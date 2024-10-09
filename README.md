# Embedding Expeerly Videos on Online Shops or Marketplaces: Developer Guide
This guide provides an overview of how to embed Expeerly videos into your online shop or marketplace. It includes examples and step-by-step instructions to assist both product owners and developers in the integration process.

## 1. Options: Youtube or Mux
Expeerly offers to Video Embedding solutions via [Youtbe](https://www.youtube.com/) Embed Links or via [Mux](https://www.mux.com/).

## 2. Embedding with Youtube
### 2.1 Embedding a YouTube Video
To embed a YouTube video, use the iframe code. This is ideal for public videos intended for widespread sharing.
```
<iframe width="560" height="315" src="https://www.youtube.com/embed/nqG3JCNkb0I?si=bikBYWxuWUS6SWCu" 
        title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; 
        encrypted-media; gyroscope; picture-in-picture; web-share" 
        referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
</iframe>
```
### 2.2 Embed examples
Galaxus shows the expeerly in their image carousel, check this [link to the Philips Avent Kit](https://www.galaxus.ch/fr/s10/product/philips-avent-kit-de-soins-pour-bebe-soin-corporel-bebe-36358432?ip=8720689021937)

Brack shows the expeerly in their image carousel, check this [link to the Philips Avent Kit ](https://www.brack.ch/philips-avent-baby-pflegeset-petrol-1614829)

## 3. Embedding with Mux
### 3.1 Embedding with Mux Streaming Links
Mux Stream provides scalable video hosting, ideal for large volumes. You can use either the .mp4 format for static video playback or the .m3u8 format for adaptive streaming.
For on-demand playback: `https://stream.mux.com/q2EyUPCM0000k3QbfjLVTmEL5N6PDL701aovfWx7QByv84/high.mp4`
For adaptive streaming (ideal for varying bandwidths): `https://stream.mux.com/q2EyUPCM0000k3QbfjLVTmEL5N6PDL701aovfWx7QByv84.m3u8`


