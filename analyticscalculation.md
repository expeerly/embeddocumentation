## What Kind of Data Do We Store?

### Storage solution
Supabase

### Channels

#### Expeerly (via Mux)
- Ochsner Sport (tracked via shop ID)
- Interdiscount (tracked via shop ID)

#### YouTube (via Integrator)
- Galaxus (tracked as external via YouTube Analytics)
- Digitec
- Brack

#### TikTok (via Integrator)
- @expeerly
- @expeerly_deutsch

#### Instagram (via Integrator)
- @expeerly
- @expeerly_deutsch

#### Facebook (via Integrator)
- @expeerly
- @expeerly_deutsch

#### Others (via CSV upload to Supabase)
- Thalia (manual tracking)
- Shop Apotheke (manual tracking)

---

## Data Points to Store (Ideal Scenario)

### General (Applicable to All Channels)
- Daily granularity
- Per individual published video (e.g., [YouTube Example](https://www.youtube.com/watch?v=7NCmm8FJD08))
- Total views
- Total watch time
- Video length
- Traffic source

### YouTube-Specific
- Traffic Source Details:
  - Geographic
  - Demographic
  - External / Search / Social
    - **External**: Brack, Digitec, Galaxus (counted as "Retail" in design of "Placement/Traffic source"  (see [here](https://jmp.sh/jeZpkbXb)) and as "Traffic source/subchannel" in the schema)
    - **Search**: Explicitly marked as search in YouTube
    - **Social**: Any source not classified as External or Search

### Mux (Expeerly.com + Direct Retail API Integrations)
- Traffic Source Details:
  - Geographic
  - Demographic
  - External / Search
    - **External**: Identified via shop ID in Mux Analytics ([example screenshot](https://jmp.sh/GPxTVYH9))
      - These views are a subset of total views for the playback ID

---

## Calculated Values

- **View-Through Rate**: Percentage of the video watched
- **Average Watch Time**: Mean duration viewed across all plays
- **Placement / Traffic Source Classification** ([design reference](https://jmp.sh/PZXfK9G0)):

  ### Retail
  - YouTube: Traffic source = External, specifically Brack, Digitec, Galaxus
  - Mux: Interdiscount and Ochsner Sport (via shop ID)
  - Thalia and Shop Apotheke (tracked manually)

  ### Search
  - YouTube: Traffic source = Search
  - Mux: All expeerly.com traffic, excluding Retail
  - TikTok: If search traffic is available and labeled

  ### Social
  - Any other traffic from YouTube, Meta (Instagram, Facebook), and TikTok that doesn't fit the Retail or Search definitions
