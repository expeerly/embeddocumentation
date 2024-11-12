To effectively track and distinguish video views originating from different online shops using Mux's streaming service, you can utilize Mux Data's custom metadata features. By assigning unique identifiers to each shop and embedding this information into the video player, you can monitor and analyze traffic sources accurately. Here's how you can implement this:

**1. Configure Custom Dimensions in Mux Data:**

Mux Data allows you to define up to ten custom dimensions, depending on your plan, to capture metadata specific to your use case. For tracking the source of video views, you can set up a custom dimension named, for example, `shop_id`. 
[See mux docs](https://docs.mux.com/guides/extend-data-with-custom-metadata)

- **Access Custom Dimensions Settings:**
  - Log in to your Mux dashboard.
  - Navigate to the **Settings** page.
  - Select the **Custom Dimensions** tab.

- **Enable and Configure a Custom Dimension:**
  - Click the edit icon next to an available custom dimension slot (e.g., `custom_1`).
  - Check the **Visible** box to make the dimension active.
  - Set the **Display Name** to `Shop ID` or another descriptive name.
  - Assign an appropriate **Category**, such as `Custom`.

This setup allows you to capture and report on the `shop_id` for each video view. 

**2. Embed the Video Player with Custom Metadata:**

When embedding the Mux video player on each online shop's website, include the unique `shop_id` in the player configuration. This ensures that each view is tagged with the corresponding shop identifier.

- **Using the `<mux-video>` Element:**
  If you're using Mux's custom video element, you can pass metadata directly as attributes:

  ```html
  <mux-video
    playback-id="Heq3vyLty8Q02H01kZ01ZvVcj7NMjLcBHi721V4bkZt75A"
    env-key="YOUR_ENV_KEY"
    metadata-video-id="video-id-1234"
    metadata-video-title="Product Demo"
    metadata-viewer-user-id="user-id-5678"
    metadata-custom-1="shop-id-001"
    controls
  ></mux-video>
  ```

  In this example, `metadata-custom-1` corresponds to the `custom_1` dimension configured earlier and is set to the unique `shop_id`. 

- **Using JavaScript SDKs:**
  If you're integrating via JavaScript, you can set the custom metadata as follows:

  ```javascript
  mux.monitor('#video-element', {
    data: {
      env_key: 'YOUR_ENV_KEY',
      video_id: 'video-id-1234',
      video_title: 'Product Demo',
      viewer_user_id: 'user-id-5678',
      custom_1: 'shop-id-001' // Unique identifier for the online shop
    }
  });
  ```

  Ensure that `custom_1` aligns with the custom dimension configured in the Mux dashboard. 

**3. Analyze Video Views by Shop:**

With custom dimensions in place, you can filter and analyze video performance metrics by `shop_id` in the Mux Data dashboard:

- Navigate to the **Metrics** section.
- Apply filters using the `Shop ID` dimension to view data specific to each online shop.

This setup enables you to monitor engagement, performance, and other key metrics for videos across different online shops, facilitating data-driven decisions and targeted improvements.

By implementing custom dimensions and embedding the appropriate metadata, you can effectively distinguish and analyze video traffic sources across various online shops using Mux's streaming service. 
