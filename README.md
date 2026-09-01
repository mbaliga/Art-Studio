# Art Studio

An open source system for art studios: presentation and management. It ships as two
self-contained web pages that any artist can copy, personalize, and put online — no
build tools, no server, no database.

## What's included

| Part | File | Who it's for | What it does |
|---|---|---|---|
| **The Gallery** | [`index.html`](./index.html) | Visitors & buyers | An immersive, walk-through gallery of the artist's work — with a viewing wall, a scrollable corridor, a "keep an eye on this piece" wishlist, a commission request form, and a camera-based "see it on your wall" size preview. |
| **The Studio** | [`studio.html`](./studio.html) | The artist & their team | A backoffice mockup for managing the collection: pricing and discounts, offer codes, buyer enquiries, and staff access levels (owner / manager / assistant). |

Both pages are a single HTML file each — CSS, JavaScript, and every artwork image are
embedded inline. There is nothing to install and nothing to build: open the file, or
host it anywhere that serves static files.

**Important:** the Studio page is a *prototype of the experience*, not a working backend.
Sign-in is simulated (any click "signs you in"), and all of its data — team members,
prices, coupons, enquiries — resets to sample data on every page reload. Likewise, the
Gallery's commission and wishlist forms validate input and show a confirmation, but they
don't actually send anything anywhere yet. See [`guides/CUSTOMIZING.md`](./guides/CUSTOMIZING.md)
for what to wire up before you rely on either page for real business.

## Quick start — set up your own gallery

1. **Get a copy.** Use this repository as a template (or just download `index.html` and
   `studio.html`) into your own project.
2. **Make it yours.** Follow [`guides/CUSTOMIZING.md`](./guides/CUSTOMIZING.md) to swap in
   your name, your artworks, your prices, and your team — every place that currently
   says "Sadhna" is listed there with the exact text to search for.
3. **Preview it.** Open `index.html` in a browser to see the gallery. For the full
   experience (including the camera preview feature), serve the folder locally instead
   of double-clicking the file — see [`guides/DEPLOYMENT.md`](./guides/DEPLOYMENT.md).
4. **Go live.** [`guides/DEPLOYMENT.md`](./guides/DEPLOYMENT.md) walks through free hosting
   options (GitHub Pages, Netlify, Vercel) and how to keep the Studio page from being
   publicly discoverable.

Each artist's copy of this repo is independent — there's no shared account, license
server, or central service to sign up for. Once it's customized and deployed, it's
entirely theirs to run.

## Documentation

- [`guides/CUSTOMIZING.md`](./guides/CUSTOMIZING.md) — every place to put your own name,
  bio, artworks, prices, offers, team, and studio details.
- [`guides/DEPLOYMENT.md`](./guides/DEPLOYMENT.md) — previewing locally and publishing for
  free, plus notes on the camera feature's HTTPS requirement and keeping the Studio
  page private.
