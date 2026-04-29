# C&R Pricebook — Deploy & Install Guide

This folder is a **complete, ready-to-publish iPad app**. It works offline once installed.

---

## Part 1 — Publish to GitHub Pages (one-time, ~10 minutes)

### Step 1. Create the repository

1. Go to **https://github.com/new** (sign in if needed).
2. **Repository name:** `cr-pricebook` (lowercase, no spaces). You can pick anything, but this name will become part of the URL.
3. Set it to **Public**. (Pages requires Public on the free plan.)
4. **Do NOT** check "Add a README". Leave everything else blank.
5. Click **Create repository**.

### Step 2. Upload the files

On the new repo page you'll see a line: **"uploading an existing file"** — click it.

Drag the **entire contents of this folder** (`CR-Pricebook-App`) into the upload area:
- `index.html`
- `manifest.json`
- `sw.js`
- `icon-192.png`
- `icon-512.png`
- `favicon-32.png`
- `DEPLOY-AND-INSTALL.md` *(optional — won't hurt anything)*

⚠️ Drag the **files**, not the folder itself. GitHub should show all 6–7 files lined up.

Scroll down, click **Commit changes**.

### Step 3. Turn on GitHub Pages

1. In your repo, click **Settings** (top tab).
2. Left sidebar → **Pages**.
3. Under **Source**, choose **Deploy from a branch**.
4. **Branch:** `main` (or `master`), **Folder:** `/ (root)`. Click **Save**.
5. Wait ~60 seconds. Refresh. You'll see:
   > **Your site is live at https://YOUR-USERNAME.github.io/cr-pricebook/**

That URL is your app. **Copy it.**

### Step 4. Test it from your computer

1. Open the URL in Chrome or Safari.
2. The pricebook should load. Enter a test customer, package prices, etc. — everything should work normally.

✅ If yes, you're ready to put it on the techs' iPads.

---

## Part 2 — Install on a Tech's iPad (do this once per iPad, ~30 seconds)

You **must** use **Safari** for this — Chrome on iPad won't let you "Add to Home Screen" the same way.

1. Open **Safari** on the iPad.
2. Go to your URL: `https://YOUR-USERNAME.github.io/cr-pricebook/`
3. Wait for it to fully load (one time only — this caches it for offline).
4. Tap the **Share** button (square with arrow pointing up, top-right of Safari).
5. Scroll down in the share menu, tap **Add to Home Screen**.
6. Confirm the name (defaults to "C&R Pricebook"), tap **Add** in the top-right.

A C&R icon will appear on the home screen. Tap it — it opens **full screen, no browser bar, like a real app**.

### Verify offline works

1. With the app installed, turn the iPad's Wi-Fi off (or put in Airplane Mode).
2. Tap the C&R Pricebook icon.
3. It should still open and work fully. *(All the math, the customer mode, everything.)*

If it does — you're done. Hand it to your techs.

---

## Part 3 — How to update the pricebook later

When you change `index.html` (new prices, new layout, etc.):

1. **Bump the cache version** in `sw.js`. Find this line:
   ```js
   const CACHE_VERSION = 'cr-pricebook-v1';
   ```
   Change `v1` to `v2`, then `v3` next time, and so on. **This is what tells the techs' iPads "there's a new version, replace the old one."**
2. Upload the new files to the GitHub repo (same drag-and-drop process — it'll ask if you want to replace).
3. Commit changes.
4. Within ~1 minute, every tech's iPad will pull the new version the next time they open it with internet.

---

## Troubleshooting

**"Add to Home Screen" doesn't appear on iPad**
- Must be Safari, not Chrome.
- Must be the actual GitHub Pages URL, not a local file.
- Scroll down in the Share sheet — it's not always visible at first.

**Tech says it won't load offline**
- It needs to be opened **once with internet** so the service worker can cache everything.
- After that first load, it works offline forever.

**You updated prices but the tech still sees the old ones**
- They need to either (a) open it once with internet, OR (b) you forgot to bump `CACHE_VERSION` in `sw.js`.

**A tech accidentally deleted the icon**
- Just repeat the install steps — Safari → URL → Share → Add to Home Screen.

---

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | The pricebook itself (Tech mode + Customer mode) |
| `manifest.json` | Tells iPad it's an installable app |
| `sw.js` | Service worker — caches the app for offline use |
| `icon-192.png` / `icon-512.png` | C&R branded home-screen icon |
| `favicon-32.png` | Browser tab icon |

---

*Built for Trinity Climate Solutions LLC d/b/a C&R Heating & Cooling.*
*"Taught by Fathers, Trusted by Families."*
