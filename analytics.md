# Analytics Feature

## Highlevel architecture

### Data storge
- Supabase

### Data integrator
- For Youtube, Tiktok, Instagram and Tiktok, To be defined (PMA/Supermetrics)
- For Mux (expeerly.com/retailer API); [mux data api](https://www.mux.com/docs/api-reference/data/metrics/list-breakdown-values)
- For Thalia/Shop Apotheke (manual CSV upload)

### Frontend
- Mobile [design](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=8266-47332&t=GqC5bw1yqZ5WbYUU-1) and desktop [design](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=8339-62765&t=1evCTWnBZGWp77bB-1) on figma
- Standalone on analytics.expeerly.com
- Next.js
- JWT token from app.expeerly.com

### Client user & product, brand, reviewer data
- On app.expeerly.com with bubble
- Needs 2 way API from bubble to supabase

---

## What Kind of Data Do We Store?

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
  - ~Demographic~ POSTPONE
  - External / Search / Social
    - **External**: Brack, Digitec, Galaxus (counted as "Retail" in design of "Placement/Traffic source"  (see [here](https://jmp.sh/jeZpkbXb)) and as "Traffic source/subchannel" in the schema)
    - **Search**: Explicitly marked as search in YouTube (counted as "Search" of "Placement/Traffic source", see [here](https://jmp.sh/h7eWaXYH))
    - **Social**: Any source not classified as External or Search

### Mux-Specific (Expeerly.com + Direct Retail API Integrations)
- Traffic Source Details:
  - Geographic
  - External / Search
    - **External**: Identified via shop ID in Mux Analytics ([example screenshot](https://jmp.sh/GPxTVYH9))
    - These views are a subset of total views for the playback ID
     
### TikTok-Specific
- Traffic Source Details:
  - Geographic
  - Search / Social
    - **Search**: Views that are specifically labelled as search
    - **Social**, all other views
   
### Instagram/Facebook-Specific
- Traffic Source Details:
  - Geographic
  - Search / Social
    - **Search**: Views that are specifically labelled as search
    - **Social**, all other views

---

## Calculated Values

- **View-Through Rate**: Percentage of the video watched
- **Average Watch Time**: Mean duration viewed across all plays
- **Placement / Traffic Source Classification** ([design reference](https://jmp.sh/PZXfK9G0)):

### Retail
- YouTube: Traffic source = External: Brack, Digitec, Galaxus
- Mux: Interdiscount and Ochsner Sport (via shop ID)
- Thalia and Shop Apotheke (uploaded manually)

### Search
- YouTube: Traffic source = Search
- Mux: All expeerly.com traffic, excluding Retail
- TikTok: If search traffic is available and labeled
- Instagram/Facebook: If search traffic is available and labeled

### Social
- Any other traffic from YouTube, Meta (Instagram, Facebook), and TikTok that doesn't fit the Retail or Search definitions

---

## Page setup

### Analytics overview
- Total views chart
- Total video views
- View through rate
- Average view length
- Total watch time
- Placement/traffic source (views)
- Number of products reviewed
- Total number of reviews
- Search traffic vs. overall traffic
- Average rating (from existing supabase video table)
- Placement/traffic source (views), detail view
- Search trafic (detail view)
- All publishing channels

### Product view (only for the relevant product)
- Average rating (from existing supabase video table)
- Total views chart
- Total video views
- View through rate
- Average view length
- Total watch time
- Placement/traffic source (views)
- Placement/traffic source (views), detail view
- Search trafic (detail view)
- All publishing channels
- Show/hide detail function

### Brand view (only for the relevant brand)
- Average rating (from existing supabase video table)
- Total views chart
- Total video views
- View through rate
- Average view length
- Total watch time
- Placement/traffic source (views)
- Placement/traffic source (views), detail view
- Search trafic (detail view)
- All publishing channels
- Show/hide detail function

---

## Filtering/Sorting

### Date range/Granualrity
- Show and select the date range (allow to comprae the same ranage back)
- Select Daily, Weekly, Monthly granularity

### Filters
- Placement/traffic source (Retail, Search, Social, as pere [here](#Retail))
- Publishing channels (All and selectable as per [here](#Channels) and design [here](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=8286-63930&t=GqC5bw1yqZ5WbYUU-1))
- Brand (from bubble, see [schema](https://dbdiagram.io/d/SchemaSimplified-684186bbba2a4ac57bfb9fa4))
- Product (from bubble, see [schema](https://dbdiagram.io/d/SchemaSimplified-684186bbba2a4ac57bfb9fa4)) 
- Reviewer (from bubble, see [schema](https://dbdiagram.io/d/SchemaSimplified-684186bbba2a4ac57bfb9fa4))

### Sorting
- Products can be sorted A-Z or Z-A

