# Haltman Static Template (Base)

This repo is a **static HTML + CSS template** designed to be:
- semantic (HTML5 structure)
- consistent (colors + typography controlled via variables)
- readable (no inline styles)
- maintainable (reusable components)
- responsive (works on small screens)
- "terminal/editorial" dark UI with subtle grid background

## Structure

```
.
├─ index.html                  # Landing page (example)
├─ page-title.html             # Title-only page (example)
├─ page.html                   # Common content page (example)
├─ blog.html                   # Blog list (cards)
├─ post.html                   # Blog post content (article)
└─ assets/
   ├─ style.css                # Theme + components (edit variables in :root)
   └─ icon-mark.svg            # Example inline icon (optional)
```

## Where to edit the "global look"

Open `assets/style.css` and edit the variables inside `:root`:

- `--font-body` / `--font-mono`
- `--c-bg`, `--c-text`, `--c-muted`, `--c-border`
- `--c-accent` (yellow marker / headings)
- `--c-link` (green links)
- spacing scale `--space-*`

## HTML patterns (the "right way")

### Page skeleton (same on all pages)

- `<header class="site-header">` : sticky navbar
- `<main>` : unique page content
- `<footer class="site-footer">` : never overlaps content (layout uses flex + `main{flex:1}`)

### Titles / text

- Main title: `<h1>` (one per page)
- Section titles: `.section__head` + `.section__marker` (the ">")
- Text: wrap in `.prose` (gives consistent margins)

### Footer

Use `.site-footer` only. Avoid `position:absolute` for footers in normal pages.
Absolute footers are the #1 reason content overlaps on small screens.

### Navbar

Navbar uses a "real" layout:
- Left: `.brand` (logo)
- Right: `.nav__links` (links)
Active page uses `aria-current="page"`.

### Logo options

You have 3 options, same CSS:

A) Text-only:
```html
<a class="brand" href="/">
  <span class="brand__name">haltman</span>
</a>
```

B) Inline SVG icon + text:
```html
<a class="brand" href="/">
  <svg class="brand__icon" viewBox="0 0 24 24" aria-hidden="true">
    <path fill="currentColor" d="M12 2l7 4v6c0 5-3 9-7 10C8 21 5 17 5 12V6l7-4z"/>
  </svg>
  <span class="brand__name">haltman</span>
</a>
```

C) Image logo + text:
```html
<a class="brand" href="/">
  <img class="brand__img" src="./assets/logo.svg" alt="Haltman logo" />
  <span class="brand__name">haltman</span>
</a>
```

### Images / GIF

Use `<figure>` so you can add captions:
```html
<figure class="figure">
  <img src="./assets/demo.png" alt="Short, useful description" loading="lazy" />
  <figcaption>Optional caption for context.</figcaption>
</figure>
```

### YouTube embed (responsive)

```html
<div class="embed">
  <iframe
    src="https://www.youtube-nocookie.com/embed/VIDEO_ID"
    title="Video title"
    loading="lazy"
    referrerpolicy="strict-origin-when-cross-origin"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen
  ></iframe>
</div>
```

### Twitter/X embed (note: external script)

Twitter requires their script. Keep it optional:
```html
<blockquote class="twitter-tweet">
  <a href="https://twitter.com/user/status/ID"></a>
</blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
```

## Tips for clean static sites

- Avoid `<br><hr><br>` as layout. Prefer a reusable `.hr`.
- Avoid inline styles (`style="color: ..."`) — use classes.
- Use rem units and CSS variables for sizing.
- Keep one CSS file, no duplicated rules.
