# Customizing your copy

Both `index.html` (the Gallery) and `studio.html` (the Studio) are plain text files —
everything in them, including the styling and the artwork photos, lives inside that one
file. You don't need a build tool to change them: open the file in any text or code
editor, use **Find** (Ctrl+F / Cmd+F) to jump to the text below, edit it, and save.

There is no link between the two files — they don't share a database or a config file.
Anything you change in one (your name, your artworks, your prices) has to be changed in
the other too, if it appears there as well. The sections below cover both.

## 1. Your name and studio identity

The sample site is filled in for a fictional artist named "Sadhna," working out of
Hyderabad. Search for these exact snippets and replace them with your own details.

**In `index.html`:**

| Find | It's the... | Replace with |
|---|---|---|
| `<title>Sadhna's art</title>` | Browser tab title | Your name / site title |
| `<div class="mark">Sadhna<em>'s</em> art</div>` | Header logo text | Your name |
| `Sadhna will let you know if a price changes` | Wishlist copy | Your name |
| `Tell Sadhna what you have in mind` | Commission form intro (appears twice) | Your name |
| `"Sadhna needs a name to reply to."` | Form validation message | Your name |
| `Sadhna will call then.` / `Sadhna will call you back` | Confirmation copy | Your name |
| `Studio in Hyderabad. Commissions take six to ten weeks depending on size.` | Fine print on the commission form | Your city and your real turnaround time |

**In `studio.html`:**

| Find | It's the... | Replace with |
|---|---|---|
| `<title>Sadhna Studio</title>` | Browser tab title | "Your Name Studio" |
| `<div class="brand">Sadhna<em>'s</em> art</div>` | Sign-in screen logo | Your name |
| `sadhna@sadhnasart.com` | Pre-filled sign-in email (appears twice) | Your email |
| `<b>Only Sadhna can get in here.</b>` | Sign-in fine print | Your name |
| `<div class="mark">Sadhna<em>'s</em> art<span>Studio</span></div>` | Sidebar logo | Your name |
| `<b>Sadhna</b>` next to "Signed in on this device" | Session label | Your name |
| `Connect @sadhnas.art` / `Connected as @sadhnas.art` | A decorative "connect your domain" button — cosmetic only, doesn't actually connect anything | Your handle, or remove the button |
| `published to sadhnasart.com` | Toast message shown after "publishing" changes | Your domain |
| `studio:["Studio","sadhnasart.com"]` | Page subtitle shown in the Studio header | Your domain |

## 2. Your artworks

Artwork photos are stored **inline as the images themselves** (a technique called a data
URI) rather than as separate image files — that's why `index.html` is a couple of
megabytes. This keeps the whole gallery to one file, at the cost of a heavier page.

**`index.html`** has its own list, near the top of the `<script>` block:

```js
const WORKS = [
  {title:"Banno", medium:"Acrylic on canvas", w:47, h:61, year:2024,
   img:"data:image/jpeg;base64,..."},
  ...
];
```

Each entry is one piece: `title`, `medium`, `w` and `h` (size in centimeters — used by
the "see it on your wall" size preview, so keep them accurate), `year`, and `img` (the
photo). To add a piece, copy an existing `{...}` entry and edit its fields. To remove
one, delete its entry.

To turn your own photo into an `img` value: export a reasonably compressed JPEG (large,
uncompressed photos will make the page slow to load — aim for well under 500 KB per
image), then convert it to base64. On macOS/Linux you can run:

```
base64 -i your-photo.jpg | tr -d '\n'
```

...and wrap the result as `"data:image/jpeg;base64,PASTE_RESULT_HERE"`. Any online
"image to base64" converter works too. You can also point `img` at a normal image URL
(e.g. `"img/your-photo.jpg"` or a link to a hosted image) instead of embedding it — the
gallery just displays whatever `img` resolves to.

**`studio.html`** has a *separate*, richer list with the same artworks (search for
`const WORKS=[`), because the Studio also tracks business details the public Gallery
doesn't show:

```js
const WORKS=[
  {title:"Banno", medium:"Acrylic on canvas", w:47, h:61, year:2024,
   price:85000, discount:0, status:"available", showPrice:true, wish:9, img:"..."},
  ...
].map(w=>({...w, id:++uid, shots:[w.img]}));
```

- `price` — in rupees, shown formatted as `₹85,000`.
- `discount` — a percentage off `price` (0 for none).
- `status` — one of `"available"`, `"reserved"`, `"sold"`, or `"draft"`.
- `showPrice` — whether the price is visible to buyers, or offered on enquiry.
- `wish` — the sample "people watching this piece" count shown in the Studio.
- `id` and `shots` are added automatically by the line above — don't set them by hand.

Keep the two lists in sync by hand: add/remove/update the same piece in both files.
There's no automatic sync between them.

## 3. Pricing, availability, and offers

Still in `studio.html`'s `WORKS` list — update `price`, `discount`, and `status` as
pieces sell, get reserved, or come back into stock.

Offer codes live in their own list, `const COUPONS=[`:

```js
{id:++couponId, code:"MONSOON10", kind:"pct", val:10, scope:0, until:"30 Sep 2026", uses:5, used:2, active:true}
```

- `kind` is `"pct"` (percent off) or `"amt"` (a flat rupee amount off).
- `scope` is `0` for "any piece," or a specific artwork's `id` (e.g. `WORKS[6].id`) to
  limit the code to one piece.
- `until` is a plain display date — it isn't validated against the real date.
- `uses` / `used` are the redemption cap and how many have been used so far.

Replace the sample codes with your own, or set the array to `[]` for none.

## 4. Your team and access levels

`studio.html`'s `const MEMBERS=[` list is who can sign in to the Studio, and
`const ROLE_PRESETS={` defines what each role is allowed to do (edit works, change
prices, publish, see buyer contact details, manage coupons, manage people). Add a
member by copying an entry and giving them a role; adjust what a role can do by editing
`ROLE_PRESETS`.

**Sign-in here is a simulation, not real security.** Clicking either sign-in button
("passkey" or "email link") logs you in immediately — there's no password, no real
passkey, and no email actually sent. The page does carry
`<meta name="robots" content="noindex, nofollow">` so search engines won't list it, but
that only keeps it out of search results — it doesn't stop anyone with the link from
opening it. Don't put real buyer contact details or unlisted pricing here until you've
added real authentication, or at minimum put the page behind hosting-level password
protection (see `guides/DEPLOYMENT.md`).

## 5. The gallery experience (`index.html`)

A few more things worth knowing about as you make the site your own:

- **View modes** — `const ENABLED_VIEWS=["rack","corridor","wall"]` controls which
  browsing layouts are offered. A few more are already built but switched off:
  `concave`, `convex`, `coverflow`, `drift` (see `const VIEW_DEFS={` for their labels).
  Add any of them to `ENABLED_VIEWS` to turn them on.
- **Color themes** — `const PALETTES = {` lists eight named moods (`monsoon`,
  `marigold`, `saltpan`, `nightbus`, `terrace`, `kotagiri`, `amma`, `ferry`), each five
  hex colors. Edit the colors, add your own named palette, or remove ones you don't
  want visitors switching to.
- **Ambient sound** — the background audio is generated in the browser (there are no
  audio files to swap out); visitors toggle it with the sound button. Look for
  `function initAudio()` if you want to adjust the tone.
- **"See it on your wall"** — a live camera (or an uploaded photo, as a fallback) with
  the artwork's image overlaid at true size using its `w`/`h` centimeters. It needs
  camera permission, which browsers only grant on `https://` or `http://localhost` —
  it will not work if you just double-click the file (see `guides/DEPLOYMENT.md`).

## 6. Forms don't send anywhere yet

The commission request form and the "keep an eye on this piece" wishlist button both
validate what a visitor types and show a confirmation screen — but neither one actually
emails, texts, or otherwise notifies you. There's no server here to send anything. The
same is true of the "sample" enquiries you'll see in the Studio (`const ENQ=[`) — they're
placeholder data, not real messages, and they don't come from your live Gallery either
(the two pages aren't connected).

Before you rely on this for real commissions, wire the form up to something that
delivers messages to you — for example a form backend such as Formspree or Getform, a
`mailto:` link, or your own server. That's the one piece of real "plumbing" this project
intentionally leaves for you to add, since the right choice depends on how you want to
be contacted.

## 7. Before you go live

- Replace the sample `WORKS`, `MEMBERS`, `COUPONS`, and `ENQ` entries in both files with
  your own (or empty lists, if you'd rather start from scratch and add pieces later).
- Search both files one more time for "Sadhna" and "sadhnasart.com" to make sure nothing
  was missed.
- Decide how commission and wishlist requests will actually reach you (see above).
