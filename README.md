[Instagram Reels Video Downloader](https://apify.com/clipminer/instagram-reels-video-downloader?fpr=data)

# Instagram Reels Video Downloader

Extract direct video URLs from Instagram Reels quickly and easily. Process single or multiple Reels in one run.

## Important Note: Authentication Required

Instagram increasingly requires authentication (cookies) to access content. Many Reels, even public ones, may fail without authentication. This Actor currently works only with publicly accessible Reels that don't require login.

## Input

```
{
  "pageUrls": [
    { "url": "https://www.instagram.com/reel/xxxxx/" },
    { "url": "https://www.instagram.com/reel/yyyyy/" }
  ],
  "proxyConfiguration": {
    "useApifyProxy": true
  }
}
```

### Input Parameters

- **pageUrls** (required): Array of Instagram Reel URLs to process

- Can be objects with `url` property: `[{ "url": "..." }]`
- Or simple strings: `["https://...", "https://..."]`
- **proxyConfiguration** (required): Apify Proxy configuration for better reliability

## Output

The Actor returns one result per input URL in the dataset:

```
[
  {
    "pageUrl": "https://www.instagram.com/reel/xxxxx/",
    "videoUrl": "https://...",
    "error": null
  },
  {
    "pageUrl": "https://www.instagram.com/reel/yyyyy/",
    "videoUrl": null,
    "error": "Unable to access this Reel. It may be private or require login."
  }
]
```

## Usage

### Single URL

```
{
  "pageUrls": [
    { "url": "https://www.instagram.com/reel/C8yT5MhJ0wN/" }
  ],
  "proxyConfiguration": {
    "useApifyProxy": true
  }
}
```

### Multiple URLs

```
{
  "pageUrls": [
    { "url": "https://www.instagram.com/reel/xxxxx/" },
    { "url": "https://www.instagram.com/reel/yyyyy/" },
    { "url": "https://www.instagram.com/reel/zzzzz/" }
  ],
  "proxyConfiguration": {
    "useApifyProxy": true
  }
}
```

## Limitations

- ✗ Does not support authentication (cookies)
- ✗ Does not handle private or login-required Reels
- ✗ Does not bypass DRM or paid content
- ✓ Only works with publicly accessible Reels
- ✓ Processes each URL independently - one failure doesn't stop others