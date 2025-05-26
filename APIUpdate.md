## 🔄 Migrating from Legacy to New API

To fetch product videos via the new API, simply update the base URL while keeping the parameters consistent.

### ✅ Step-by-Step

#### 1. Legacy API Format: 
`https://app.expeerly.com/api/1.1/wf/get-product-videos-processed/?access_key=YOUR_ACCESS_KEY&gtin=GTIN_CODE`

#### 2. New API Format:
`https://api.expeerly.com/api/videos?gtin=GTIN_CODE&access_key=YOUR_ACCESS_KEY`


### Example Migration

| Product           | GTIN           | Legacy API                                                                                      | New API                                                                                   |
|-------------------|----------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| Puma Future 8     | 4067983093241  | `https://app.expeerly.com/api/1.1/wf/get-product-videos-processed/?access_key=233i2q1l23w837w1k29we4mn8ui03gh&gtin=4067983093241` | `https://api.expeerly.com/api/videos?gtin=4067983093241&access_key=233i2q1l23w837w1k29we4mn8ui03gh` |
| Sony Brava 7      | 4548736159815  | `https://app.expeerly.com/api/1.1/wf/get-product-videos-processed/?access_key=233i2q1l23w837w1k29we4mn8ui03gh&gtin=4548736159815` | `https://api.expeerly.com/api/videos?gtin=4548736159815&access_key=233i2q1l23w837w1k29we4mn8ui03gh` |

### Key Changes:
- **Base URL updated** from `app.expeerly.com/api/1.1/wf/get-product-videos-processed`  
- **Query params** (`gtin`, `access_key`) remain the same
- **Field names** check the table below
- Now uses the new production domain: `api.expeerly.com`



| Field (API legacy)               | Field (API new)           |
| -------------------------------- | ------------------------- |
| `_id`                            | `id`                      |
| `gtin_text`                      | `gtinEan`                 |
| `product_name_text`              | `productName`             |
| `mux_playback_id_text`           | `muxPlaybackId`           |
| `assetgroup_custom_review`       | `assetGroup`              |
| `rating_number`                  | `rating`                  |
| `reviewer_first_name_text`       | `reviewerFirstName`       |
| `reviewer_last_name_text`        | `reviewerLastName`        |
| `reviewer_profile_pic_image`     | `reviewerProfilePic`      |
| `status_option_reviewer_status`  | `status`                  |
| `videoupload1_custom_videoupload`| `videoUpload`             |
| `Created Date` / `Modified Date` | `createdAt` / `updatedAt` |
| `product_custom_product2`        | `product`                 |
