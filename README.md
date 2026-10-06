# zangormo.github.io — Zangormo Util

Static developer website for **Zangormo Util**, served by GitHub Pages at **https://zangormo.github.io/** (user-site repository `zangormo.github.io`).

Plain HTML + CSS, no frameworks, no JavaScript, no build step. Push to the default branch and GitHub Pages publishes it.

## Structure

```
/index.html                    Home ("Zangormo Util")
/homepoker-cashier/index.html  HomePoker Cashier app page
/about/index.html              About / portfolio (CV page)
/404.html                      Not-found page (GitHub Pages serves it automatically)
/style.css                     Shared styles
/assets/favicon.svg            Favicon + placeholder app icon (green spade)
/assets/screenshots/           App screenshots (you add these)
/assets/Ilja_Birjukovs_CV.pdf  CV for download (you add this)
/app-ads.txt                   AdMob app-ads.txt (must stay in the root)
/.nojekyll                     Disables Jekyll processing
```

All internal links are root-relative (`/about/`), so the site only works when served from the domain root — i.e. from the `zangormo.github.io` repository, not from a project repository.

The privacy policy lives in a **separate repository** and is linked as an external URL: https://zangormo.github.io/poker_cashier_privacy_page/ — do not create a `poker_cashier_privacy_page` file or folder here, it would conflict.

## app-ads.txt

`app-ads.txt` must contain exactly one line, plain text, no comments:

```
google.com, pub-<your publisher id>, DIRECT, f08c47fec0942fa0
```

The file holds the AdMob Publisher ID. Keep the format unchanged and do not add comment lines. After publishing, check https://zangormo.github.io/app-ads.txt.

## Google Play developer website

In Play Console (Store presence → Store settings → Contact details), set the **Website** to exactly:

```
https://zangormo.github.io
```

AdMob crawls `app-ads.txt` from the root of that domain.

## Google Play "coming soon" flag

The Play button is controlled by a single attribute on the `<html>` tag of each page that shows it:

- `/homepoker-cashier/index.html`
- `/index.html` (app card on the home page)

```html
<html lang="en" data-play-live="false">   <!-- "Coming soon to Google Play" (disabled) -->
<html lang="en" data-play-live="true">    <!-- "Get it on Google Play" → Play Store link -->
```

Default is `false`. Flip both pages to `true` when the app goes public. Store link: https://play.google.com/store/apps/details?id=com.zango.pokertracker

## Screenshots

Screenshots live in `/assets/screenshots/` as `screenshot-1.jpg` … `screenshot-6.jpg` and are shown in that order as a stack of cards on `/homepoker-cashier/` (tap or swipe the front card, use the arrows, or pick a screen from the list).

To add, remove or reorder screenshots, edit the `<ol class="shots">` list in `/homepoker-cashier/index.html`: give each image an `alt` text describing the screen, and each `<li>` a `data-title` and a one-line `data-desc` shown next to the stack. The script at the bottom of the page builds the rest. Use simple file names: **no `#`, spaces or other special characters** (`#` starts a URL fragment, so `#1.jpg` can never load). Crop the phone status bar off the top; the gallery frame is 576 × 1224 (portrait). Keep them small (≈ 576 px wide JPG/WebP).

## CV

Place the PDF at `/assets/Ilja_Birjukovs_CV.pdf` (exact name). The "Download CV" button on `/about/` links to it.

## Remaining TODOs

- [ ] `/about/index.html`: **Personal Finance Tracker** repository link is a placeholder (`href="#"`, marked with a `TODO` comment). Replace it with the real repository URL.
- [ ] Optional: replace `/assets/favicon.svg` usage for the app icon with the real launcher icon (e.g. `/assets/app-icon.png`) and add an `og:image` (1200×630 PNG) for nicer link previews.
- [ ] Set `data-play-live="true"` once the app is public.

## Local preview

Don't open the HTML files directly (`file:///…`): root-relative paths like `/style.css` then point to the root of the disk, so styles and images won't load. Run a local server from the repository folder instead:

```
py -m http.server 8000
```

and open http://localhost:8000/
