# Prashanth Sandela — Personal Site Guide

A reference for deploying and maintaining `prashanthsandela.com` on GitHub Pages,
and the design system that gives the site its identity. Keep this in the repo so
future-you (or anyone helping) stays consistent.

---

## Part 1 — Deploy

### 1. Create the repository
- Repo name (exact, lowercase): **`prashanthsandela.github.io`**
- Visibility: **Public** (required for free GitHub Pages)
- This exact name makes it a *user site* served at the root — which is what a
  personal homepage needs, and what a custom domain maps to cleanly.

### 2. Add the site files
Drop these at the **root** of the repo (not in a subfolder):
- `index.html` — the site itself
- `resume.pdf` — optional; the Résumé button already links to this name
- `SETUP-AND-DESIGN.md` — this file, for reference

Easiest path with no terminal: open the repo → **Add file → Upload files** →
drag them in → **Commit changes**.

### 3. Turn on Pages
Repo → **Settings** → **Pages** → **Source:** *Deploy from a branch* →
Branch: **`main`**, Folder: **`/ (root)`** → **Save**.
Wait ~1 minute. Live at `https://prashanthsandela.github.io`.

### 4. Point your domain
1. Settings → Pages → **Custom domain** → enter `prashanthsandela.com` → Save.
   (This creates a `CNAME` file in the repo — leave it there.)
2. At your domain registrar / DNS host, set these records:

   | Type  | Host / Name | Value                     |
   |-------|-------------|---------------------------|
   | A     | `@`         | `185.199.108.153`         |
   | A     | `@`         | `185.199.109.153`         |
   | A     | `@`         | `185.199.110.153`         |
   | A     | `@`         | `185.199.111.153`         |
   | CNAME | `www`       | `prashanthsandela.github.io` |

   > These are GitHub's published Pages IPs. Verify current values at
   > docs.github.com if it's been a while — they change rarely but do change.
3. Back in Settings → Pages, tick **Enforce HTTPS** once the certificate issues
   (can take up to a few hours).
4. DNS changes can take 15 min – 48 hrs to fully propagate.

> **Migration note:** repointing DNS is what actually moves the live domain off
> Blogger. Until you change the records, `prashanthsandela.com` keeps showing the
> old site even though the new one is already live at the `.github.io` URL.

---

## Part 2 — The design system

The site has a deliberate identity. When you add or change anything, pull values
from here so it stays coherent instead of drifting.

### Concept
A **"console / instrument panel"** aesthetic drawn from your actual domain:
real-time ML serving. Deep navy, precise monospaced data, one quiet warm accent.
The look should feel *measured and engineered*, not decorative.

### Signature element
The **status readout strip** in the hero — the monospaced metric panel with the
pulsing dot. This is the one thing meant to be memorable. Keep it prominent and
keep everything else calmer than it. Don't add a second attention-grabber that
competes with it.

### Color tokens
Defined as CSS variables at the top of `index.html`. Use the variable, never a
raw hex, so a future change stays global.

| Token       | Hex       | Use                                      |
|-------------|-----------|------------------------------------------|
| `--ink`     | `#0E1424` | Page background (deep navy, not black)   |
| `--surface` | `#141C30` | Raised panels / cards                    |
| `--line`    | `#243049` | Hairline dividers, borders               |
| `--paper`   | `#E8ECF4` | Primary text                             |
| `--muted`   | `#8390AB` | Secondary text, labels                   |
| `--cyan`    | `#54C7F0` | Primary accent — links, numbers, hovers  |
| `--coral`   | `#FF7A66` | Warm accent — used **once**, status dot  |

Rule of thumb: `--cyan` is the working accent. `--coral` is a single spark —
resist using it elsewhere, or it stops being special.

### Typography
Three faces, each with one job:

| Role    | Font           | Used for                              |
|---------|----------------|---------------------------------------|
| Display | Space Grotesk  | Headlines, section titles, your name  |
| Body    | Inter          | Paragraphs, readable prose            |
| Utility | JetBrains Mono | Labels, metrics, nav, dates, the readout |

The mono face is the personality carrier — it's what makes the site read as
"engineer," not "generic portfolio." Keep it on data and labels; keep prose in
Inter so it stays readable.

### Structure
Four numbered sections, in this order and for this reason:
1. **About** — who you are, in your voice
2. **Selected work** — projects, each led by a real *metric* (your edge)
3. **Writing** — the reputation engine; grows over time
4. **Connect** — links out

The numbering (`01–04`) is meaningful because it's a real reading sequence, not
decoration. If you add sections, keep them in a logical order and renumber.

### Motion
Minimal and purposeful: the pulsing status dot, subtle card lift on hover, a
slight indent on writing links. `prefers-reduced-motion` is respected — don't
add animation that ignores it.

### Accessibility floor (don't drop below this)
- Works down to mobile (single-column at small widths — already handled).
- Visible keyboard focus (the cyan outline — keep it).
- Reduced motion respected.
- Text keeps strong contrast on the navy background.

---

## Part 3 — Keeping it alive

The site is the hub, not the engine. What builds reputation is the **Writing**
section filling up. To add a post, duplicate one entry in the `.posts` block:

```html
<a class="post" href="LINK-TO-POST">
  <span class="date">2026 · 03</span>
  <span class="title">Your post title here</span>
  <span class="arrow" aria-hidden="true">→</span>
</a>
```

Delete the `.empty-note` line once you have a couple of real posts.

### A short maintenance rhythm
- Ship a technical writeup on a cadence you can sustain, then link it here.
- Update the hero metrics only with numbers you can defend publicly.
- Keep the résumé PDF current (`resume.pdf` at repo root).
- Every edit is just a commit — the site rebuilds automatically in ~1 minute.

---

*One file, no framework, no build step. Edit `index.html`, commit, done.*
