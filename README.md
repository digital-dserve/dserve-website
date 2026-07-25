# Dserve Website — Editing & Deployment Guide

This is a **static HTML website** (no database, no WordPress, no monthly hosting fee).
It was rebuilt from your old WordPress backup, keeping the real Dserve content, images, and the Bosa theme's look and feel.

## What's in this folder

```
dserve-site/
  index.html          Homepage
  about.html          Our Story
  initiatives.html    Enable Arts & Paatshala
  team.html           Our Team
  volunteer.html      Volunteer page
  donate.html         Donation details
  contact.html        Contact page
  blog.html           Blog listing
  blog/               Individual blog post pages
  css/style.css       All site styling (colors, fonts, layout)
  images/             Photos and logos
```

Every page is a plain `.html` file you can open by double-clicking, or edit with any text editor (even Notepad/TextEdit). There's no build step.

## Placeholders you still need to fill in

Search each file for the word `PLACEHOLDER` (Cmd+F in a text editor) — these mark spots where real information was missing from the old WordPress export:

- **Contact page / footer**: real office address and phone number (the old site never had these filled in)
- **Donate page**: a UPI QR code image, if you have one
- **Contact page**: the contact form currently only looks like a form — see "Making the contact form work" below.

## How to make changes (no coding knowledge needed)

1. Open the `.html` file for the page you want to change in any text editor.
2. Find the sentence you want to change (use Cmd+F / Ctrl+F to search for a word from it).
3. Type your replacement text between the same tags, save the file.
4. If you're using GitHub + Netlify (see below), just upload/commit the changed file — the live site updates automatically within a minute.

## Maintaining the blog

All blog posts live as individual files in the `blog/` folder, and `blog.html` is just a listing page of cards linking to them. Nothing here depends on WordPress, a database, or any specific host — it's all plain files, so this works identically whether you're testing locally or already live on Netlify.

### Editing an existing blog post
1. Open the relevant file in `blog/` (e.g. `blog/inclusivity-in-disability.html`) in any text editor.
2. Find the text you want to change (Cmd+F / Ctrl+F), edit it, and save.
3. If the post's title changes, also update the link text for that post on `blog.html` and on `index.html` (homepage blog preview), so they stay in sync — they're just plain text, not auto-linked.
4. If deployed via GitHub+Netlify (see below), commit/upload the changed file(s) — Netlify rebuilds automatically within about a minute.

### Adding a brand-new blog post
1. **Duplicate a template.** Copy any existing file in `blog/`, e.g. `blog/inclusivity-in-disability.html`, and rename the copy to describe your new post using lowercase words and hyphens, e.g. `blog/world-disability-day-2026.html`. (Keep it inside the `blog/` folder — the header/footer links in every post file use `../` to reach `css/`, `images/`, and the top-level pages, so a file moved elsewhere will break those links.)
2. **Edit the new file:**
   - Update the `<title>` tag in `<head>` and the visible `<h1>` heading to your new post's title.
   - Update the date line under the title.
   - Replace the body paragraphs with your new content.
   - If you want an image in the post, add it to `images/` first (see "Adding new images" below), then reference it as `../images/your-file.jpg`.
   - Leave the "&larr; Back to Blog" link and the header/footer exactly as they are — just copy them from the template.
3. **Add a card to the blog listing.** Open `blog.html`, copy one whole `<div class="blog-card">...</div>` block, paste it into the grid, and edit its title, date, excerpt, and the two `href="blog/..."` links (one on the title, one on "Read more") to point at your new file.
4. **(Optional) Feature it on the homepage.** `index.html` has a 3-post preview in its "Insights & Updates" section — swap one of the existing `<div class="blog-card">` entries there for your new post if you want it to show up on the homepage too.
5. **Publish.** If deployed via GitHub+Netlify, add/commit the new `blog/your-file.html` plus your edited `blog.html` (and `index.html` if changed) — Netlify picks up the change and republishes automatically within about a minute, no separate "build" step needed.

### Adding new images
Just drop the image file into the `images/` folder (keep file names lowercase, no spaces — use hyphens, e.g. `event-photo-2026.jpg`). Reference it from a top-level page as `images/event-photo-2026.jpg`, or from a file inside `blog/` as `../images/event-photo-2026.jpg`.

## Deploying for free — step by step

### Step 1: Put the site on GitHub (free)
1. Create a free account at github.com if you don't have one.
2. Create a new repository (e.g. `dserve-website`).
3. Upload this entire `dserve-site` folder's contents to that repository (GitHub's web interface lets you drag-and-drop files — no command line needed).

### Step 2: Connect it to Netlify (free hosting)
1. Create a free account at netlify.com (you can sign up using your GitHub account).
2. Click "Add new site" → "Import an existing project" → choose your GitHub repo.
3. Leave build settings blank/default (this is a plain HTML site, nothing to "build").
4. Click Deploy. Netlify gives you a free `something.netlify.app` link within a minute — check the site works there first.

### Step 3: Point your domain (dserve.org.in) at Netlify
1. In Netlify: Site settings → Domain management → Add custom domain → enter `dserve.org.in`.
2. Netlify will show you DNS records to set up (usually an "A record" and/or "CNAME").
3. Log into Hostinger → DNS settings for dserve.org.in → add the records Netlify gave you.
4. DNS changes can take a few hours to a day to fully apply. Netlify also gives you free HTTPS (the padlock icon) automatically once this is done.

You keep paying Hostinger only for the domain name itself (unchanged) — hosting is now free on Netlify.

### Step 4 (optional, for easier future editing): Add a CMS
Once the site is live on Netlify, we can add **Decap CMS** — a free tool that gives you a simple login page (`yoursite.com/admin`) with form fields to add/edit blog posts and pages, without touching HTML at all. This is a quick follow-up setup once the site above is live — just ask when you're ready.

## Making the contact form actually send emails

The contact form on `contact.html` is currently just the visual layout — plain HTML forms can't send email by themselves. Once the site is on Netlify, this is a small config change (Netlify has a free built-in form-handling feature) — flag this to me when you're ready to wire it up.

## A note on sensitive information

The donation page includes your real bank account and UPI details, since these were already public on the live site for accepting donations. If you ever need to change banks or take this down temporarily, just edit `donate.html` directly.
