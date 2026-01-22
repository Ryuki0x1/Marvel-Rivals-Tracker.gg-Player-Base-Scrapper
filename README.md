# Marvel-Rivals-Tracker.gg-Player-Base-Scrapper
A Python + Playwright automation tool to scrape Top 3 Heroes and All-Time Best Rank for Marvel Rivals players from tracker.gg, using in-game names only.  Built with DOM-accurate selectors, live saving, and resume support, designed to work reliably on modern React-based pages.

# 🕷️ Marvel Rivals Tracker.gg Scraper

A **Python + Playwright automation tool** to scrape **Top 3 Heroes** and **All-Time Best Rank** for **Marvel Rivals** players from **tracker.gg**, using **in-game names only**.

Built with **DOM-accurate selectors**, **live saving**, and **resume support**, designed to work reliably on modern React-based pages.

---

## ✨ Features

* ✅ Uses **ONLY In-Game Name (IGN)** (no Discord tags, no guesses)
* ✅ Direct profile access via tracker.gg canonical URLs
* ✅ Scrapes:

  * **Top 3 Heroes** (from *Top Heroes* section)
  * **All-Time Best Rank** (from *All-Time Best* stat block)
* ✅ **Live save** after every player
* ✅ **Resume-safe** (can restart without losing progress)
* ✅ Cloudflare-friendly (persistent browser profile)
* ✅ Outputs **Excel + plain text**
* ✅ Handles missing / private data gracefully

---

## 📁 Project Structure

```
MarvelRivalsTracker/
├── tracker_marvel_rivals_live_final.py   # Main scraper
├── players.txt                           # Input (IGN | UID)
├── marvel_rivals_top3.xlsx               # Output (Excel)
├── marvel_rivals_top3.txt                # Output (Text)
├── browser_profile/                      # Persistent Playwright profile
└── README.md
```

---

## 📥 Requirements

* **Windows / Linux / macOS**
* **Python 3.10+**
* **Google Chrome / Chromium**

### Python packages

```bash
pip install playwright pandas openpyxl
playwright install chromium
```

---

## 📄 Input Format

### `players.txt`

Each line must be:

```
IGN|UID
```

Example:

```
mewomewo|852823175
woofwoof|1383151760
moomoo|2091738905
```

⚠️ Notes:

* IGN must be **exactly** the in-game name as shown on tracker.gg
* UID is stored only for reference/output
* No Discord names, no emojis, no extra fields

---

## 🌐 Profile URL Used

The scraper **only** uses this canonical format:

```
https://tracker.gg/marvel-rivals/profile/ign/{IGN}/overview?season=12
```

* IGN is URL-encoded automatically
* No search pages
* No UID-based profiles

---

## 📊 Data Collected

### 1️⃣ Top 3 Heroes

* Scraped from the **“Top Heroes”** v3-card
* Hero names are extracted from:

  ```
  img[alt]
  ```
* First 3 heroes in DOM order
* Missing heroes → `"N/A"`

### 2️⃣ All-Time Best Rank

* Anchored to:

  ```
  <span class="caption">All-Time Best</span>
  ```
* Rank value extracted from:

  ```
  img[alt]
  ```
* Example value:

  ```
  Grandmaster III // S2.5
  ```
* If not present → `"N/A"`

---

## 📤 Output

### Excel (`marvel_rivals_top3.xlsx`)

Columns:

```
Name | UID | Hero 1 | Hero 2 | Hero 3 | All-Time Best Rank
```

### Text (`marvel_rivals_top3.txt`)

```
IGN | UID | Hero1 | Hero2 | Hero3 | All-Time Best Rank
```

Example:

```
adil | 852823173 | Iron Man | Scarlet Witch | Loki | Grandmaster III // S2.5
```

---

## ▶️ How to Run

```bash
python tracker_marvel_rivals_live_final.py
```

### First run

* Chromium will open
* Complete Cloudflare check **once**
* Do **not** close the browser manually

---

## 🔁 Resume Support

* If the script stops or crashes:

  * Re-run it
  * Already processed IGNs are skipped automatically
* Output files are **updated after every player**

---

## ⏱️ Timing & Rate Limits

* Random delay: **4–6 seconds per profile**
* Designed to stay under tracker.gg anti-bot thresholds
* Faster delays may trigger Cloudflare

---

## ⚠️ Known Limitations (Honest)

* Some profiles **do not have**:

  * Ranked history
  * All-Time Best stat
* In those cases, `"N/A"` is correct
* tracker.gg may change DOM structure in the future
* This tool does **not** bypass private profiles

---

## 🧠 Technical Notes

* No `inner_text()` is used for critical data
* All scraping is **DOM-anchored**, not heuristic
* Uses semantic attributes (`alt`, captions) for stability
* Designed specifically for **React + dynamic layouts**

---

## 🔐 Legal & Ethical Disclaimer

This project is for:

* Personal use
* Data analysis
* Educational purposes

Respect tracker.gg’s Terms of Service.
Do not abuse or overload their infrastructure.

---

## 🚀 Future Improvements

* Rank normalization (tier + division)
* Full hero list scraping
* Team-wise analytics
* Adaptive delay on Cloudflare detection
* Screenshot logging on failure

---

## 🧾 License

MIT License
Use responsibly.

---

If you want, next I can:

* Generate a **`.gitignore`**
* Write a **commit history suggestion**
* Help you publish this cleanly on GitHub
* Add **example outputs** for the README

Just say the word.
