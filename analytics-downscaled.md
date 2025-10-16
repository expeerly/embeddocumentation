# Analytics Feature

## Highlevel architecture

### Data storge
- Supabase

### Data integrator
- For Youtube, use Youtube data API
- Tiktok, Instagram and Tiktok, use Supermetrics
- For Mux (expeerly.com/retailer API); [mux data api](https://www.mux.com/docs/api-reference/data/metrics/list-breakdown-values)

### Frontend
- Standalone on analytics.expeerly.com
- Next.js
- See [here](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=8921-75637&t=2513qwe1EyaK0lFu-0)
- Use 2 breakpoints
  - @media (max-width: 1024px) for smaller screens, keep landscape version, just remove space left right, and make container for views smaller, see [here](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=9342-72472&t=2513qwe1EyaK0lFu-0)
  - @media (max-width: 640px), use the mobile vertical version, see [here](https://www.figma.com/design/MU9nzvKpZjcbRV2Wjs5ozC/CompleteApp-PlayerUX?node-id=9342-71411&t=2513qwe1EyaK0lFu-0)
- Please note, the responsive design doesn't need to be pixel perfect, just make sure that the content is not cut off or overlapping using the browser emulator
- JWT token from app.expeerly.com/bubble that allows the customer to see their own data
- Create a special token for expeerly admins that allows to see the data of ALL customers

---

## What Kind of Data Do We Store?

### Channels

#### Expeerly (via Mux)
- Ochsner Sport (tracked via shop ID)
- Interdiscount (tracked via shop ID)

#### YouTube (via Integrator)
- Galaxus (tracked as external via YouTube Analytics)
- Digitec (tracked as external via YouTube Analytics)
- Brack (tracked as external via YouTube Analytics)

#### TikTok (via Integrator)
- @expeerly
- @expeerly_deutsch

#### Instagram (via Integrator)
- @expeerly
- @expeerly_deutsch

#### Facebook (via Integrator)
- @expeerly
- @expeerly_deutsch

---

## Data To Show

### General
- Views only
- On the dashboard, we'll always show aggreated monthly levels
- For channels where daily granularity is available, sum up a running month to a total

---

## Calculated Values

- **Placement / Traffic Source Classification** 

### Retail
- YouTube: Traffic source = External: Brack, Digitec, Galaxus
- Mux: Interdiscount and Ochsner Sport (via shop ID tag)

### Search
- YouTube: Traffic source = YoutubeSearch
- Mux: All expeerly.com traffic, excluding Retail tagged via shop ID

### Social
- Any other traffic from YouTube that is not labelled as Search or Retail (=youtube external "brack", "digitec", "galaxus")
- Meta (Instagram, Facebook)
- Tiktok

---

## Page setup

### Analytics overview
- Total video views
- By default show the the complete running year
- Placement/traffic source (Retail, Search, Social)
- Placement breakdown

---

## Filtering/Sorting

### Date range/Granualrity
- Show and select the date range
- The earliest month available is September 2025
- Date selection is not possible for future months
- Per default we show monthly granularity
  - For channels where daily granularity is available, sum up a running month to a total

### Filters
- Brand per customer (only single select possible)
- Product (multi select possible, the user needs to choose a brand first)
- For expeerly super admin, all customers and thus all brands are available

