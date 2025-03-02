# Runway Automation

You can use Runway Automation directly form APIFY platform [apify.com/igolaizola/runway-automation](https://apify.com/igolaizola/runway-automation)

## 🎬 What does Runway Automation do?

Runway Automation enables you to automate AI video generation on [RunwayML](https://www.runwayml.com) without manual intervention. With this actor, you can:

- 🤖 Process multiple video prompts in bulk
- 🎥 Generate videos either from text prompts (text-to-video) or from images (image-to-video)
- ⚡ Handle multiple jobs concurrently
- ⏳ Manage random wait times between operations
- 📁 Generate an album HTML file for easy video browsing and downloading

### Video Generation Modes

- **Image-to-Video:**  
  If you supply image URLs (via the `images` parameter) or a Google Drive folder URL (via the `googleDriveFolder` parameter), videos will be generated using your images. If you also provide text prompts, they will be used as additional input. When there are fewer prompts than images, the prompts will be repeated (looped) to ensure every image is paired with a prompt.

- **Text-to-Video:**  
  If no images or Google Drive folder is provided, the generation will be based solely on the text prompts you supply.

## 🔑 Prerequisites

Before using this actor, you need:

1. An active Runway subscription
2. Your Runway session token for authentication
3. The [LocalStorage Exporter Chrome extension](https://chromewebstore.google.com/detail/localstorage-exporter/gnfhbfoioepibbdcbikgcmenpdfgohmd)

## 🚀 Setup Guide

### Getting Your Runway Session Token

1. Install the LocalStorage Exporter Chrome extension.
2. Log in to [app.runwayml.com](https://app.runwayml.com).
3. Click on the LocalStorage Exporter extension icon.
4. Click **Export to Clipboard**.
5. Copy the exported session data and paste it into the actor's `session` field.

### Running the Actor

1. Paste your session token into the actor's `session` input field.
2. Enter your desired video prompts or specify image URLs (or a Google Drive folder URL) for image-to-video conversion.
3. Configure generation options (choose mode, model, aspect ratio, video duration, etc.).
4. Select a proxy from your country (recommended).
5. Run the actor.

## ⚙️ Input Parameters

| Parameter            | Type    | Description                                                                                                                                           | Default                                 |
| -------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| `session`            | String  | Your Runway session token from [app.runwayml.com](https://app.runwayml.com) (required)                                                                | -                                       |
| `folder`             | String  | Runway folder where videos will be generated. **Note:** This folder must be manually created in Runway.                                               | Generations                             |
| `prompts`            | Array   | List of text prompts to generate videos.                                                                                                              | -                                       |
| `images`             | Array   | _(Optional)_ List of image URLs for image-to-video conversion. You can also use a Google Drive folder URL instead.                                    | -                                       |
| `googleDriveFolder`  | String  | _(Optional)_ Google Drive folder URL containing images for video generation. The folder must be publicly shared.                                      | -                                       |
| `mode`               | Select  | Generation mode: "explore" (slow, doesn't consume credits) or "credits" (fast, consumes credits)                                                      | explore                                 |
| `model`              | Select  | Model to generate videos. _(Note: Vertical videos are only available for 'Gen 3 Alpha Turbo', and text-to-video is only available for 'Gen 3 Alpha')_ | gen3-alpha                              |
| `aspectRatio`        | Select  | Aspect ratio of the generated video. Options: "1280x768" (16:9 Horizontal) or "768x1280" (9:16 Vertical)                                              | 1280x768                                |
| `seconds`            | Select  | Duration of the generated video. Options: "5s" or "10s"                                                                                               | 10s                                     |
| `concurrency`        | Integer | Number of concurrent jobs                                                                                                                             | 1                                       |
| `minWait`            | Integer | Minimum wait time between operations (seconds). A random wait time is chosen between the minimum and maximum values.                                  | 5                                       |
| `maxWait`            | Integer | Maximum wait time between operations (seconds).                                                                                                       | 10                                      |
| `jobTimeout`         | Integer | Maximum time to wait for job completion (seconds). If a job takes longer than this timeout, it will be skipped.                                       | 300                                     |
| `proxyConfiguration` | Object  | Configuration for selecting proxies to use.                                                                                                           | Uses Apify Residential proxy by default |

## 📋 Output Format

The actor provides results in a structured JSON format. An example output looks like this:

```json
[
  {
    "album_url": "https://api.apify.com/v2/key-value-stores/1Ht4z6r0m1OfBqZs1/records/album.html#619775b2-1f53-409e-ad1d-5a8336b138b8",
    "prompt": "Modern residential houses in nature, minimalist and elegant architecture, large glass facades, surrounded by trees, mountains, or lakes with sunlight streaming through",
    "url": "https://cdn.runwayml.com/619775b2-1f53-409e-ad1d-5a8336b138b8/video.mp4",
    "preview_url": "https://cdn.runwayml.com/619775b2-1f53-409e-ad1d-5a8336b138b8/preview.jpg",
    "job_id": "619775b2-1f53-409e-ad1d-5a8336b138b8",
    "image_url": "https://drive.usercontent.google.com/download?id=14ur340HEc31z4z1Y0C1_"
  }
]
```

## 🎥 Accessing Generated Videos

The actor saves an `album.html` file to the KeyValue store, providing an interface for easy browsing and downloading of your generated videos. You can access it by:

- Clicking any "Album URL" field in the results table.
- Navigating to **Run > Storage > KeyValueStore** and locating the `album.html` file.

The album interface offers several features:

- **Filtering:** Search videos by prompt text or other metadata.
- **Batch Operations:** Select multiple videos for batch downloads.
- **Detailed Viewing:** Open videos in new tabs for closer inspection.
- **Download Options:** Download selected videos as a ZIP file.

Here's an example album showcasing some generated videos so you can see how your results will be displayed: [Browse Example Gallery](https://igolaizola.github.io/runway-automation/)

## ⚠️ Usage Guidelines and Best Practices

### Account Safety

- Automating Runway accounts may lead to termination.
- Use this actor only for batch jobs you would normally perform manually.
- Avoid running the automation continuously (24/7).
- Always follow Runway's terms of service.

### Performance Optimization

- Start with 1–2 concurrent jobs and adjust based on performance.
- Use proxies from your region to improve reliability.
- Set appropriate job timeouts based on your selected generation mode.
- Regularly update your session token if you plan long sessions.

### General Tips

- Test your setup with a small batch of prompts before scaling up.
- Use clear, descriptive prompts to keep your results organized.
- Monitor job success rates and tweak settings as needed.
- Note that failed jobs are logged but won’t stop the entire process.

## 💳 How much will it cost to use Runway Automation?

Apify provides you with $5 free usage credits every month on the [Apify Free plan](https://apify.com/pricing). You can try and test Runway Automation for free with these credits.

If you plan to use it regularly, consider subscribing to one of Apify’s plans. We recommend the [$49/month Personal plan](https://apify.com/pricing) which covers the costs of Runway Automation along with numerous executions.
