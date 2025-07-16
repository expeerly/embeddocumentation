#### What kind of data we want to store?
- Channels:
  - Expeerly (Mux)
    - Ochsner Sport (as per shop id)
    - Interdiscount (as per shop id)  
  - Youtube
    - Galaxus (external source as per YT analytics)
    - Digitec
    - Brack
  - Tiktok expeerly
  - Tiktok expeerly_deutsch
  - Instagram expeerly
  - Instagram expeerly_deutsch
  - Facebook expeerly
  - Facebook expeerly_deutsch 
  - Thalia
  - Shop Apotheke

#### Data points to store (ideal scenario)
- For all channels 
  - on a daily basis
  - Per individual published video e.g https://www.youtube.com/watch?v=7NCmm8FJD08
  - Total views
  - Total watch time
  - Video length
  - Traffic source
- For Youtube
  - Traffic source (geographic, demographic, external/search/social)
    - For external we should specifically track Brack, Digitec and Galaxus placements (External is what is called "Retail" in the design, or "Traffic source/subchannel in the database schema)
    - If a traffic source from Youtube is neither "External" nor "Search", count as "Social"
 - For mux (expeerly.com and direct retail API integrations)
  - Traffic source (geographic, demographic, external/search)
    - For external the traffic source is indicated by the shop-id in the mux analytics: https://jmp.sh/GPxTVYH9 it is just a part of total views on the given playback ID (External is what is called "Retail" in the design, or "Traffic source/subchannel in the database schema)

#### Calculated values
  - View through rate (% of video watched)
  - Average watch time (average total video length)
  - Placement/traffic source (see design: https://jmp.sh/PZXfK9G0)
    - Retail: Youtube (Traffic source "external" with Brack, Digitec, Galaxus), Mux (Interdiscount, OchsnerSport, as per shop ID), Thalia (manual), Shop Apotheke (manual)
   - Search: Youtube (all traffic labeled as "Search"), expeerly.com (Mux) all traffic minus above retail traffic, Tiktok search if available and labelled as such
   - Social: All other traffic from Youtube, Meta and Youtube that is not part of above criteria
