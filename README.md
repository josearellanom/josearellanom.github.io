# josearellanom.com

Personal academic website of Jose Arellano Martorellet. Plain HTML and CSS, no build step, hosted free on GitHub Pages.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | About page (photo, bio, contact links, research themes, link to the Research page) |
| `research.html` | Publications and working papers |
| `cv.html` | Education, experience, awards and grants, presentations, teaching, public writing, skills |
| `tennis.html` | Hidden tennis game (opened by clicking the small gold dot next to the photo) with a top-5 leaderboard stored in Firebase |
| `guess.html` | Hidden guessing game (opened by clicking the small teal ⅔ next to the photo): guess two-thirds of the average, one guess per visitor per monthly round, guesses stored in Firebase |
| `style.css` | All colors, fonts, and spacing (colors are at the top) |
| `images/` | `portrait.webp` (cut-out photo on the About page), `profile.jpg` (photo shown when the site is shared on social media), `favicon.png`, `favicon-32.png` and `apple-touch-icon.png` (browser-tab and phone home-screen icon: the scientist emoji from Noto Emoji, Apache License 2.0), `favicon-tennis.svg` (tab icon on the tennis page), `favicon-guess.svg` (tab icon on the guessing game), `face.png` (face on the computer's paddle in the game) |
| `sitemap.xml`, `robots.txt` | Tell search engines which pages to index. If you add a new page, add its address to `sitemap.xml` |
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
- Each paper's colored dot comes from `style="--dot: var(--amber)"` on its `<article>` (use `--amber`, `--teal`, or `--coral` for the three research themes).
- The header and footer are repeated on each page. If you change one (for example, adding a nav link), change it on all three.
- The moon/sun button next to the name switches light and dark mode and remembers each visitor's choice. Dark-mode colors are defined twice near the top of `style.css` (once for the device setting, once for the button); change both when editing them.
- After editing `style.css`, bump the number in `style.css?v=5` (to `v=6`, and so on) in the four HTML files, so visitors' browsers load the new version instead of an old cached copy.
- To change colors, edit the variables at the top of `style.css`. The three research-theme colors are `--amber` (attention and engagement), `--teal` (credibility and beliefs), and `--coral` (from intention to action). A paper that belongs to two themes gets two dots.

## Tennis leaderboard

- The leaderboard is stored in a free Firebase (Firestore) database, in a collection called `scores`.
- The connection settings are the `firebaseConfig` block near the top of the script in `tennis.html`. While `apiKey` is empty, the game still works but scores are not saved.
- To remove an unwanted entry, open the Firebase console → Firestore Database → `scores`, and delete the document. Visitors cannot edit or delete scores.

## Guessing game

`guess.html` uses the same Firebase project as the tennis leaderboard, in a collection called `guesses`. Each guess stores the round (for example `2026-11`), the number, an optional name, and the time.

- **Rounds** are calendar months, Eastern time. The first round runs from launch to October 31, 2026 (`FIRST_ROUND` near the top of the script). Each browser gets one guess per round.
- **Winners** are worked out when the page loads: the guess closest to two-thirds of that round's average wins (ties go to whoever guessed first). Guesses sent after a round closed are ignored.
- **Removing a guess:** in the Firebase console, open Firestore Database → `guesses` and delete the document.
- **Firestore rules:** the `guesses` block below must be inside your rules, next to the `scores` block:

```
match /guesses/{id} {
  allow read: if true;
  allow create: if request.resource.data.keys().hasOnly(['round', 'guess', 'name', 'createdAt'])
    && request.resource.data.round is string
    && request.resource.data.round.matches('^20[0-9]{2}-[0-9]{2}$')
    && request.resource.data.guess is int
    && request.resource.data.guess >= 0 && request.resource.data.guess <= 100
    && request.resource.data.name is string
    && request.resource.data.name.size() <= 16
    && request.resource.data.createdAt == request.time;
  allow update, delete: if false;
}
```

## Visitor stats

Visits are counted with GoatCounter (no cookies). Dashboard: https://josearellanom.goatcounter.com. The snippet is the last `<script>` before `</body>` on index, research, and cv. Add the same line to any new page you want counted.
