# Humanities Innovation Lab — website

The lab's site, as a Jekyll project deployed to GitHub Pages. It replaces the Wix
site at `humanitiesinnovationlab.ca`, from which all content, images, and URLs
were migrated.

---

## Running it locally

You need Ruby (3.1+). Then:

```bash
bundle install
bundle exec jekyll serve
```

Open <http://localhost:4000>.

---

## Deploying

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the site
and publishes it. One-time setup: **Settings → Pages → Source → GitHub Actions**.

### Pointing the custom domain at it

The site currently expects to live at `https://humanities-innovation-lab.github.io`.
To serve it from `humanitiesinnovationlab.ca` instead:

1. Add a file named `CNAME` at the repository root containing one line:
   `humanitiesinnovationlab.ca`
2. Set `url: "https://humanitiesinnovationlab.ca"` in `_config.yml`.
3. At the domain registrar, point the apex record at GitHub Pages' IPs and add a
   `www` CNAME to `humanities-innovation-lab.github.io`.
4. In **Settings → Pages**, enter the custom domain and tick *Enforce HTTPS*.

Do this only once you are ready to move the domain off Wix.

---

## Layout of the project

```
├── _config.yml            site settings, nav-independent metadata
├── _data/                 all editable content that isn't a blog post
│   ├── members.yml        lab members: name, role, photo, bio (HTML), links
│   ├── projects.yml       the three lab projects
│   ├── publications.yml   books, chapters, articles
│   ├── events.yml         workshops, lectures, reading groups
│   └── resources.yml      the HIL Resources Index, grouped by topic
├── _includes/             head, nav, footer, land acknowledgement
├── _layouts/              default, page, post
├── _posts/                112 blog posts migrated from Wix
├── assets/
│   ├── css/main.css       the whole stylesheet (design tokens at the top)
│   └── img/               193 images, mirrored from Wix
├── index.html             home
├── about-hil.html         Projects        → /about-hil/
├── about-us.html          People          → /about-us/
├── publications.html      → /publications/
├── events.html            → /events/
├── courses.html           Resources       → /courses/
├── blog.html              archive + filter → /blog/
└── contact.html           → /contact/
```

### URLs are deliberately unchanged

The page paths and the post permalink (`/post/:title/`) reproduce the Wix ones, so
existing links, citations, and search results keep working. Renaming a file would
break them — change `permalink:` in the page's front matter instead, and only on
purpose.

---

## Editing content

**A new blog post.** Add `_posts/YYYY-MM-DD-some-slug.md`:

```markdown
---
layout: post
title: "Your title"
date: 2026-08-01
categories: ["News"]        # News, Blogs, or Tutorials — or omit entirely
image: /assets/img/your-image.jpg
description: One or two sentences; shown on cards and used for search results.
---

Body text in Markdown.
```

The blog page's filter chips are generated from whichever categories are actually
in use, so a new category needs no extra wiring.

**A member, project, publication, event, or resource.** Edit the matching file in
`_data/`. Nothing else needs touching — every page loops over these lists. Member
bios are HTML so that inline links survive.

**Images.** Drop them in `assets/img/` and reference them as
`/assets/img/filename.jpg`. Keep the long edge at or under about 1800px.

**Design.** All colours, fonts, and spacing are CSS custom properties in the
`:root` block at the top of `assets/css/main.css`. Change them there and the whole
site follows.

---

## Notes on the migration

- **Content.** All 112 blog posts came across with their text, formatting, links,
  categories, dates, and images. Page copy, the thirteen member bios, three
  project descriptions, one publication, eleven events, and ten resource entries
  were carried over verbatim.
- **Images** were pulled from the Wix CDN and now live in `assets/img/`, so the
  site will not break when the Wix subscription lapses. They were downscaled to
  1800px and re-encoded (279 MB → 73 MB).
- **One post needs attention.** *Writing. Easy and hard* had its body in an
  embedded Wix HTML component (an iframe), which is not recoverable from the page
  source. The file carries a note saying so; paste the text in.
- **Three Wix slips were corrected**: "Co-direrctor" → "Co-director";
  "Yu-Chai Pai" → "Yu-Chia Pai" in that bio's closing line; and a doubled article
  in "in the The Cultural, Social, and Political Thought program". Everything else
  is verbatim, including Barbara's "$333.000" and the wording of each bio.
- **Fonts.** The Wix site used Raleway with Avenir Light. Avenir is not freely
  licensed, so Nunito Sans stands in for the body text.
- **The Wix "Members" page** was a login-gated Wix members area with no public
  content, so it was not carried over.
- **Categories.** 55 posts carry a category on Wix (News 40, Blogs 9,
  Tutorials 6); the other 57 have none there either. The blog filter therefore
  includes an "Uncategorised" chip.
