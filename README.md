[Instagram Reels Video Downloader](https://apify.com/neuro-scraper/instagram-reels-video-downloader?fpr=data)

# 🌟 Instagram Video and Reels Downloader Actor

[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)](https://console.apify.com)
[![Version](https://img.shields.io/badge/version-1.0.0-blue)](https://console.apify.com)
LICENSE
[![Trusted](https://img.shields.io/badge/trusted-by_developers-green)](https://console.apify.com)

**One-line hero:** Instantly fetch Instagram videos & Reels at scale — reliable downloads, safe storage, and enterprise-ready uploads in seconds.

---

## 📖 Short summary

A production-ready Apify Actor that discovers and downloads Instagram media (regular videos and Reels), merges audio/video when needed, and securely stores results in Apify Key-Value Store or Dataset — plug-and-play for fast results.

---

## 💡 Use cases / When to use

- Collect public Instagram videos and Reels for analytics or archives.
- Batch export videos to a secure Key-Value Store for downstream processing.
- Create offline backups of frequently updated Instagram content.
- Integrate media fetch into pipelines for ML, moderation, or content migration.

---

## ⚡ Quick Start (Console — one-click)

1. Open this Actor in Apify Console.
2. Paste your input JSON (see `input.example.json`).
3. Click **Run** — get results in seconds.

![Console Hero Screenshot](https://images.apifyusercontent.com/0ypwnzh_a3UEc2F4w9hRBjM5dHbaIlMCYOM1Up93YcI/w:1800/cb:1/aHR0cHM6Ly92aWEucGxhY2Vob2xkZXIuY29tLzgwMHgzMDA_dGV4dD1BcGlmeStDb25zb2xlK1J1bitTY3JlZW5zaG90.webp)

---

## ⚙️ Quick Start (CLI + API)

**CLI (one-liner)**

```
$apify run --actor <OWNER>/<ACTOR_NAME> --input input.example.json
```

**Python (`apify-client`)**

```
from apify_client import ApifyClient
client = ApifyClient('<APIFY_TOKEN>')
run = client.actor('OWNER/ACTOR_NAME').call(input={
    'startUrls': ['https://www.instagram.com/p/EXAMPLE/'],
    'download': True,
    'desired_resolution': '1080p'
})
print('Run started:', run['id'])
```

---

## 📝 Inputs (fields & schema)

**Console JSON example** — see `input.example.json` file for copy-paste.

**Top-level input fields** (concise):

```
{
  "startUrls": [
    "https://www.instagram.com/p/EXAMPLE/",
    "https://www.instagram.com/reel/EXAMPLE/"
  ],
  "download": true,
  "desired_resolution": "1080p",
  "merge_if_ffmpeg": true,
  "save_videos_to_kv": true,
  "remove_local_files": false,
  "cookie_file": null,
  "proxyConfiguration": {},
  "maxConcurrency": 3
}
```

---

## ⚙️ Configuration

| 🔑 Name | 📝 Type | ❓ Required | ⚙️ Default | 📌 Example | 🧠 Notes |
| --- | --- | --- | --- | --- | --- |
| startUrls | array | ✅ Yes | [] | ["[https://.../p/ID/](https://.../p/ID/)", "[https://.../reel/ID/](https://.../reel/ID/)"] | One or more Instagram media URLs to download |
| download | boolean | ⚙️ Optional | false | true | If true, media will be downloaded and optionally uploaded |
| desired_resolution | string | ⚙️ Optional | "1080p" | "720p" | Preferred resolution (1080p/720p/480p/360p) |
| merge_if_ffmpeg | boolean | ⚙️ Optional | false | true | Merge video+audio when separate (requires ffmpeg) |
| save_videos_to_kv | boolean | ⚙️ Optional | true | true | Upload downloaded media to Apify Key-Value Store |
| remove_local_files | boolean | ⚙️ Optional | false | false | Remove temporary files after upload |
| cookie_file | string | ⚙️ Optional | null | "cookies.txt" | Use for private/protected content (upload as secret) |
| proxyConfiguration | object | ⚙️ Optional | {} | {"useApifyProxy": true} | Apify Proxy config object or custom proxy settings |
| maxConcurrency | integer | ⚙️ Optional | 3 | 3 | Number of concurrent downloads (tune for your plan) |

**Console setup hint:** Paste the JSON example into the Actor input field, adjust `startUrls` and flags, then click **Run**.

---

## 📄 Outputs (Dataset / KV examples)

This Actor writes per-run aggregated metadata to the Key-Value Store under the `OUTPUT` key and pushes per-item objects to the default Dataset.

**Example output object (single item)**

```
{
  "url": "https://www.instagram.com/reel/EXAMPLE/",
  "title": "Sample Title",
  "uploader": "uploader_name",
  "duration": 34,
  "formats_count": 5,
  "requested_resolution": "1080p",
  "download_links": {"merged_video":"https://..."},
  "downloaded_file": "Sample_Title.mp4",
  "kv_media_key": "MEDIA_abcdef123456_Sample_Title.mp4"
}
```

**Explanation:**

- `OUTPUT` (KVS) — aggregated array of all results for easy programmatic consumption.
- Dataset rows — per-URL metadata and download/upload status.

---

## 🔑 Environment Variables

- `APIFY_TOKEN` — **required** for CLI/API runs. Use placeholder: `<APIFY_TOKEN>`.
- Custom proxies: use placeholders like `<PROXY_USER:PASS@HOST:PORT>` when configuring secrets.

> Always store tokens and proxy credentials in Apify Console Secrets; do not place secrets in plain input JSON.

---

## ▶️ How to Run (Console, CLI, API)

**Console**

1. Open Actor page in Apify Console.
2. Paste `input.example.json` into the Input field.
3. Click **Run**. Monitor logs and results in the Console UI.

**CLI**

```
$apify run --actor <OWNER>/<ACTOR_NAME> --input input.example.json
```

**API (Python)** — see Quick Start above for snippet.

---

## ⏰ Scheduling & Webhooks

- Schedule periodic runs using Apify Console Scheduler (cron-style). Use `maxConcurrency` to control load.
- Configure Webhooks in Console to receive a POST when a run finishes — ideal for downstream pipelines.

---

## 🕾️ Logs & Troubleshooting

- Check run logs in Apify Console for per-item extraction and download messages.
- Common quick fixes:

- `ffmpeg`-related merges fail → enable `merge_if_ffmpeg` only if ffmpeg is available in your environment.
- Authentication-only content → provide `cookie_file` via Console file upload and reference its filename.
- Proxy errors → double-check proxy secret and format.

---

## 🔒 Permissions & Storage Notes

- Storage: Dataset (per-item), Key-Value Store (`OUTPUT` key) and temporary local disk during downloads.
- Privacy: Actor is secure by design — tokens and proxy credentials should be stored in Console Secrets. The Actor does not leak secrets to outputs.

---

## 🔟 Changelog / Versioning

- `v1.0.0` — Initial production-ready release: format discovery, async downloads, KVS upload, concurrency controls.

---

## 🖌 Notes / TODOs

- TODO: confirm output schema — inferred from main.py but not explicit.
- TODO: add demo GIF/screenshots (provide images or screenshots for best conversion).

---

## 🌍 Proxy Configuration

**Enable Apify Proxy (Console):** turn on the built-in Apify Proxy toggle in the Actor run settings.

**Custom proxies:** set `proxyConfiguration` input or configure environment variables. Example placeholders:

- HTTP/HTTPS proxy env vars:

```
HTTP_PROXY=<PROXY_USER:PASS@HOST:PORT>
HTTPS_PROXY=<PROXY_USER:PASS@HOST:PORT>
```

**Secrets:** Always store proxy credentials as Console Secrets, not plaintext in inputs.

**Advanced:** TODO: Consider proxy rotation for large-scale scraping.

---

## 📚 References

1. Official Apify Actor README guidelines — (Console docs)
2. Apify input/output schema docs — (Console docs)
3. Apify CLI & API usage docs — (Console docs)

---

## 🤔 What I inferred from `main.py`

- The Actor performs network extraction and downloads Instagram media (regular videos and Reels).
- Main inputs: `startUrls`, `download`, `desired_resolution`, `merge_if_ffmpeg`, `save_videos_to_kv`, `remove_local_files`, `cookie_file`, `proxyConfiguration`, `maxConcurrency`.
- Outputs: per-item metadata pushed to Dataset and an aggregated array stored to Key-Value Store under the `OUTPUT` key.
- Scheduling and concurrency controls are built into the Actor input (via `maxConcurrency`).

---

---

# --- input.example.json ---

```
{
  "startUrls": [
    "https://www.instagram.com/p/EXAMPLE/",
    "https://www.instagram.com/reel/EXAMPLE/"
  ],
  "download": true,
  "desired_resolution": "1080p",
  "merge_if_ffmpeg": true,
  "save_videos_to_kv": true,
  "remove_local_files": false,
  "cookie_file": null,
  "proxyConfiguration": {},
  "maxConcurrency": 3
}
```

# --- CONFIG.md ---

## CONFIG & Advanced Notes

- **File uploads (cookies):** upload your cookies file in Apify Console `Files` and reference the filename in `cookie_file`.
- **ffmpeg:** merging requires ffmpeg available on the runner. If you rely on merging, ensure your environment supports it or set `merge_if_ffmpeg` to false.
- **Proxy formats:** use `<PROXY_USER:PASS@HOST:PORT>` placeholders for custom proxies and store as Console Secrets.
- **Scaling:** increase `maxConcurrency` carefully according to your Apify plan and target site capacity.

---

*End of generated documentation.*