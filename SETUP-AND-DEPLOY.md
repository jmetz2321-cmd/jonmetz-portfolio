## How this site was originally created (Cursor-first workflow)

Before this repo existed, the site was built iteratively in Cursor with the following high-level steps:

1. **Start from a prompt and empty folder**
   - Opened a new workspace (`portfolio/`) in Cursor.
   - Prompted Cursor to create a **single-page portfolio website** with:
     - `index.html` for structure and content.
     - `styles.css` for custom styling layered on top of Tailwind via CDN.
     - `script.js` for scroll animations, stat counters, and mobile nav.
   - Used additional prompts to shape the design (hero, case studies, AI coaching section, colors, glows, dark theme).

2. **Iteratively refine content and layout in Cursor**
   - Edited `index.html` many times via natural-language instructions in Cursor:
     - Added and removed sections (Experience, Testimonials, Patents & Awards).
     - Introduced the **AI Coaching** section (Leland Supercoach, 4.9/5.0 rating, bullets, testimonials).
     - Updated hero copy (companies, revenue stat, “How I Use AI” GitHub CTA).
     - Simplified coaching bullets and steps after multiple `/debate` panels (PM, UX, EM, AI Analyst).
   - Adjusted `styles.css` for:
     - A warm dark theme, hero glows, noise overlay, and glassmorphic cards.
     - Mobile responsiveness (font sizes, padding, flex-wrap, safe-area insets).
     - Accessibility (focus-visible outlines, `prefers-reduced-motion` support).
   - Updated `script.js` to:
     - Remove an experimental testimonial carousel.
     - Gate stat animations behind `prefers-reduced-motion`.
     - Handle nav highlighting and mobile menu toggling.

3. **Use Cursor’s browser + local server to preview**
   - Ran `python3 -m http.server 8765` from `portfolio/`.
   - Used Cursor’s integrated browser (and later, a real phone) to:
     - Inspect mobile layout, safe-areas, and tap targets.
     - Debug hero alignment and centered vs. left-aligned content.

4. **Sync content to a markdown source of truth**
   - Maintained `WEBSITE-CONTENT.md` as a text source for:
     - Hero copy.
     - Case study summaries and metrics.
     - AI coaching bullets, testimonials, and calls-to-action.
   - Periodically synced `index.html` to match `WEBSITE-CONTENT.md` (and vice versa).

5. **Create a Git repo and push to GitHub**
   - Initialized git in the local folder and committed the site files.
   - Created the GitHub repo `jonmetz-portfolio` and pushed `main`.
   - Later cloned that repo into a clean workspace and copied the final `portfolio/` files into it so GitHub Pages could serve from the repo root.

6. **Enable GitHub Pages and treat `main` as production**
   - Enabled GitHub Pages for `jonmetz-portfolio` (source: `main`, folder: `/`).
   - From then on, the workflow became:
     - Edit in Cursor → preview locally → `git add` → `git commit` → `git push`.
     - Wait 1–3 minutes for GitHub Pages to redeploy.

The rest of this document describes how to reproduce and extend this setup yourself, starting from the cloned repo.

---

## Overview

This document explains how to set up, edit, preview, and deploy this portfolio + AI coaching website using Cursor and GitHub Pages.

The repo name in the examples is `jonmetz-portfolio`, owned by `jmetz2321-cmd`. Adjust names if you fork or rename.

---

## 1. Prerequisites

- **Accounts**
  - GitHub account (with SSH or HTTPS access configured).
- **Local tools**
  - `git` installed (`git --version`)
  - Python 3 (`python3 --version`) for a simple local server
  - Cursor IDE installed and configured

---

## 2. Clone the repository

From a terminal on your machine:

```bash
cd "/Users/<your-username>/Documents"    # or any workspace directory you prefer

# Clone via SSH (recommended)
git clone git@github.com:jmetz2321-cmd/jonmetz-portfolio.git

cd jonmetz-portfolio
```

You should now see:

```bash
ls
# README.md
# SETUP-AND-DEPLOY.md
# WEBSITE-CONTENT.md
# favicon.svg
# headshot.png
# index.html
# script.js
# styles.css
```

---

## 3. Open the project in Cursor

1. Open Cursor.
2. Use **File → Open Folder…**.
3. Select the `jonmetz-portfolio` folder you just cloned.
4. Cursor will index the folder and show:
   - `index.html` (structure + content)
   - `styles.css` (custom styling)
   - `script.js` (scroll reveal, nav, stat animations)
   - `WEBSITE-CONTENT.md` (content reference)

You can now use the Cursor chat and inline tools to edit files.

---

## 4. Run a local preview server

From a terminal in the repo folder:

```bash
cd "/Users/<your-username>/Documents/jonmetz-portfolio"
python3 -m http.server 8765
```

Then:

- Open `http://localhost:8765/` in your desktop browser to preview.
- To test on a phone on the same Wi‑Fi:
  - Find your Mac’s IP address (e.g. `192.168.1.10`).
  - Open `http://192.168.1.10:8765/` in Safari/Chrome on your device.

Stop the server with `Ctrl+C` in the terminal when finished.

---

## 5. Editing the site in Cursor

### 5.1 HTML (`index.html`)

- **Hero & copy**: Edit the main content, stats, and CTAs.
- **Business Impact**: Update case study text, metrics, and labels.
- **AI Coaching**: Adjust headline, bullets, testimonials, and Calendly URL.

All sections are wrapped in a shared `site-container` class so they stay aligned and responsive; keep new sections inside `div.site-container` for consistent layout.

### 5.2 CSS (`styles.css`)

- Global colors, glows, and noise overlay are defined at the top.
- `.site-container` controls consistent max-width and gutters across sections.
- Media queries and utility classes handle mobile tweaks (e.g. centering, safe-area).

Make small, intentional changes and verify them locally in the browser before committing.

### 5.3 JavaScript (`script.js`)

- Handles:
  - Scroll reveal animations via `IntersectionObserver`
  - Stat counter animation (respecting `prefers-reduced-motion`)
  - Mobile menu toggle and active nav links

Only change JS if you want to modify these behaviors.

---

## 6. Committing changes with git

After you’ve edited files in Cursor and verified them locally:

```bash
cd "/Users/<your-username>/Documents/jonmetz-portfolio"

# See what changed
git status

# Stage files (example: HTML + CSS + JS)
git add index.html styles.css script.js

# Commit with a clear message
git commit -m "Describe the change, e.g. update coaching copy and hero layout"
```

If you accidentally staged unwanted files, you can unstage with:

```bash
git restore --staged <file>
```

---

## 7. Push to GitHub

Once you have a commit:

```bash
git push
```

If this is the first push from your machine, Git may prompt you to authenticate (via browser or Personal Access Token). After that, subsequent pushes should be automatic.

Your changes are now in the `main` branch of the GitHub repo `jmetz2321-cmd/jonmetz-portfolio`.

---

## 8. Configure GitHub Pages (one-time)

This repo is designed to deploy via **GitHub Pages** as a project site.

1. Go to the repository on GitHub:
   - `https://github.com/jmetz2321-cmd/jonmetz-portfolio`
2. Click **Settings**.
3. In the left sidebar, choose **Pages**.
4. Under **Source**:
   - Select `Deploy from a branch`.
   - Branch: `main`.
   - Folder: `/ (root)`.
5. Click **Save**.

After 1–3 minutes, GitHub will expose:

- `https://jmetz2321-cmd.github.io/jonmetz-portfolio/`

The Pages settings page will show the exact URL and deployment status.

---

## 9. Updating the live site

Once GitHub Pages is configured, the deployment pipeline is:

1. **Edit in Cursor** (HTML/CSS/JS).
2. **Preview locally** at `http://localhost:8765/`.
3. **Commit and push** to `main`:

   ```bash
   git add .
   git commit -m "Short description of change"
   git push
   ```

4. Wait ~1–3 minutes.
5. Visit:
   - `https://jmetz2321-cmd.github.io/jonmetz-portfolio/`
   - On mobile, if it looks cached, use a private/incognito tab or add a cache-buster like `?v=2`:
     - `https://jmetz2321-cmd.github.io/jonmetz-portfolio/?v=2`

---

## 10. Optional: Use as your root GitHub Pages site

If you want this portfolio at:

- `https://jmetz2321-cmd.github.io`

You must use the special user-site repo name:

1. Create or use a repo named **`jmetz2321-cmd.github.io`**.
2. Copy the contents of `jonmetz-portfolio` into that repo’s root (same file layout).
3. Enable Pages for that repo with:
   - Branch: `main`
   - Folder: `/ (root)`

Then your root user URL will serve this site, and `jonmetz-portfolio` can remain as the code/source repo or as a separate project site.

---

## 11. Recommended workflow summary

1. Clone repo and open in Cursor.
2. Run `python3 -m http.server 8765` to preview locally.
3. Make changes to `index.html`, `styles.css`, `script.js` as needed.
4. Verify changes in the browser (desktop + mobile, or using your phone over Wi‑Fi).
5. Commit and push to `main`.
6. Wait a couple minutes for GitHub Pages to redeploy.
7. Validate the live site at `https://jmetz2321-cmd.github.io/jonmetz-portfolio/`.

