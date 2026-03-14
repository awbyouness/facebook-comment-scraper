# 📦 Facebook Comment Scraper

A Selenium-based Python scraper to extract comments from **any Facebook post URL format** — no API key required.

Built with `undetected-chromedriver` to bypass bot detection, with a **universal URL normalizer** that converts all Facebook link types into a scrapable format before extracting comments.

---

## ✨ Features

- ✅ Works with **all Facebook URL formats**: `/posts/`, `/photo/?fbid=`, `/videos/`, `/reel/`, `/permalink/`
- ✅ Automatically normalizes URLs to unlock full comment access (photo URLs only show a subset of comments without this)
- ✅ Switches comment sort to **"All comments"** automatically
- ✅ Scrolls to the bottom of the comment section to capture everything
- ✅ Handles posts with 0 comments gracefully — no crashes
- ✅ Saves results to CSV with original URL preserved for traceability
- ✅ Stealth mode via `undetected-chromedriver` to avoid detection

---

## 🧠 How the URL Normalizer Works

Facebook comment access is limited on media URLs (`/photo/`, `/reel/`, etc.) because they load a lightweight viewer. The scraper solves this by detecting the URL type and resolving it to the full post format:

```
Any Facebook URL
        │
        ▼
 Detect URL type
        │
        ├─── /posts/ (numeric)  ──► Pass through directly
        ├─── /posts/ (named)    ──► Load page → extract owner_id from HTML
        ├─── /photo/?fbid=      ──► Load page → extract owner_id + story_fbid
        ├─── /videos/           ──► Load page → extract owner_id + post_id
        ├─── /reel/             ──► Load page → extract owner_id + post_id
        └─── /permalink/        ──► Follow redirect → re-detect
                │
                ▼
    https://facebook.com/{owner_id}/posts/{post_id}
                │
                ▼
        Full comment section unlocked ✅
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- Google Chrome installed

### Usage

1. Open `facebook_comment_scraper.ipynb` in Jupyter
2. Run the **Setup** cell — a Chrome window will open
3. Come back to the notebook and run the remaining cells
4. Feed your list of URLs into `all_fb_links` and run the main loop
5. Comments are saved to `facebook_comments_output.csv`

---

## 📁 Project Structure

```
facebook-comment-scraper/
│
├── facebook_comment_scraper.ipynb   # Main notebook
├── requirements.txt                 # Python dependencies
└── README.md                        # This file
```

---

## 📊 Output Format

The output CSV contains:

| Column | Description |
|---|---|
| `comment` | The extracted comment text |
| `Origin_of_comms` | The original URL as provided |
| `Normalized_URL` | The resolved `/posts/` URL used for scraping |

---

## 📦 Dependencies

```
selenium
undetected-chromedriver
pandas
openpyxl
```

---

## ⚠️ Disclaimer

This tool is intended for **personal and research use only**. Scraping Facebook may be against their [Terms of Service](https://www.facebook.com/terms.php). Use responsibly and only on pages/content you have permission to access.

---

## 👨‍💻 Author

**[Awby]** — Data Scientist & Digital Marketing Analyst  
+7 years experience in marketing analytics, automation, and data science.

📧 awbyybwa93@gmail.com

---

*If this was useful, consider ⭐ starring the repo!*
