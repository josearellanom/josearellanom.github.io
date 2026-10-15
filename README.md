# josearellanom.com

Personal academic website of Jose Arellano Martorellet. Plain HTML and CSS, no build step, hosted free on GitHub Pages.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | About page (photo, bio, research themes, current work, contact links) |
| `research.html` | Publications, working papers, presentations |
| `cv.html` | Education, awards and grants, teaching |
| `style.css` | All colors, fonts, and spacing (colors are at the top) |
| `images/` | `portrait.webp` (cut-out photo on the About page), `profile.jpg` (photo shown when the site is shared on social media), `favicon.svg` (browser-tab icon) |
| `CNAME` | Tells GitHub Pages to serve the site at josearellanom.com. Don't delete it |

## Before you publish

1. **Photo:** the About page uses `images/portrait.webp`, a photo with the background removed. `images/profile.jpg` is only used for link previews on social media.
2. **CV (later):** save your CV as `cv.pdf` in the main folder, then in `cv.html` remove the `<!--` and `-->` around the "Download full CV" line.

You can preview the site anytime by double-clicking `index.html`.

## Put it online (one-time setup, about 20 minutes)

### 1. GitHub

1. Create a free account at github.com.
2. Click **New repository**. Name it `josearellanom.github.io` (replace `josearellanom` with your username if it differs). Make it **Public**. Create it.
3. On the empty repository page, click **uploading an existing file**. Drag in everything *inside* this folder (the files and the `images` folder, not the folder itself). Click **Commit changes**.
4. Go to **Settings → Pages**. Under "Build and deployment", choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.

### 2. Porkbun

1. Log in, go to **Domain Management**, and find josearellanom.com.
2. Turn off the free **Link In Bio** service on the domain (it currently redirects your domain to an l.ink page).
3. Open **DNS** for the domain. Delete any existing records for the root domain or `www` that point to Porkbun's parking or link pages (A, ALIAS, or CNAME records). Leave the email-forwarding (MX) records alone if you set up forwarding.
4. Add these records:

| Type | Host | Answer |
|---|---|---|
| A | *(leave blank)* | 185.199.108.153 |
| A | *(leave blank)* | 185.199.109.153 |
| A | *(leave blank)* | 185.199.110.153 |
| A | *(leave blank)* | 185.199.111.153 |
| CNAME | www | `yourusername.github.io` |

### 3. Finish in GitHub

1. Back in **Settings → Pages**, the custom domain should already read `josearellanom.com`. If not, type it in and save.
2. Wait for the DNS check to turn green (minutes to a few hours).
3. Tick **Enforce HTTPS** once it becomes clickable (can take up to a day).
4. Recommended: in your account **Settings → Pages → Add a domain**, verify josearellanom.com. This stops anyone else from claiming your domain on GitHub.

## Editing later

- On github.com, open a file, click the pencil icon, make the change, and click **Commit changes**. The live site updates within a minute or two.
- To add a paper, copy an `<article class="entry"> … </article>` block in `research.html` and edit it. Comments in the files mark where things go.
- The header and footer are repeated on each page. If you change one (for example, adding a nav link), change it on all three.
- To change colors, edit the variables at the top of `style.css`. The three research-theme colors are `--amber`, `--teal`, and `--coral`.
- The "Current work" list on the About page is a short highlight. When a paper changes status, update it both there and in `research.html`.
