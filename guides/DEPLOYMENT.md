# Previewing and publishing

Both pages are static HTML — there's no build step, no server-side code, and no
dependencies to install. "Deploying" this project just means putting the two files
somewhere that can serve them over the web.

## Previewing on your own computer

You can simply double-click `index.html` or `studio.html` to open them in a browser.
That's enough to check your text and artwork edits.

One feature needs more than that: the Gallery's **"see it on your wall"** camera
preview. Browsers only allow camera access on a "secure context" — a page served over
`https://`, or over `http://localhost` — never on a file opened directly
(`file:///...`). To test that feature locally, serve the folder instead of opening the
file:

```
# from inside the project folder
python3 -m http.server 8000
```

...then visit `http://localhost:8000/index.html`. Any other local server works too
(e.g. the VS Code "Live Server" extension, or `npx serve`).

## Publishing for free

Any of these work well for a two-page static site. Pick whichever you're already
comfortable with — there's no functional difference between them for this project.

### GitHub Pages (uses this repository directly)

1. Push your customized `index.html` and `studio.html` to your repository's default
   branch (they need to stay at the root of the repo, not inside a folder).
2. In the repository's **Settings → Pages**, set the source to that branch and the
   root folder.
3. GitHub will publish your Gallery at `https://<your-username>.github.io/<repo-name>/`
   and your Studio at the same address with `/studio.html` appended. Both are served
   over HTTPS automatically, so the camera preview will work.

### Netlify or Vercel

Drag the folder containing both files onto Netlify's or Vercel's dashboard (or connect
your GitHub repository for automatic redeploys on every push). Either one serves static
files over HTTPS with no configuration needed.

### A custom domain

All three options above support attaching a domain you own — look for "custom domain"
in GitHub Pages' repository settings, or in your Netlify/Vercel site settings, and
follow the DNS instructions they give you.

## Keeping the Studio page private

`studio.html` carries a `<meta name="robots" content="noindex, nofollow">` tag, so
search engines won't list it — but that's the only protection it has. Its sign-in
screen is a simulation (see `guides/CUSTOMIZING.md`), not real access control, so anyone
who has or guesses the URL can open it.

If you want it genuinely private before adding real authentication, keep it out of
reach at the hosting level instead:

- **Netlify**: enable password protection on the deploy (available on paid plans), or
  put `studio.html` on a separate, unlisted subdomain you don't link to publicly.
- **Vercel**: use "Password Protection" in the project's settings (also a paid feature),
  or similarly keep it on an unlisted URL.
- **GitHub Pages**: has no built-in password option — if you need real privacy here,
  host the Studio page separately on a provider that offers one, rather than publishing
  it alongside the public Gallery.

None of these are a substitute for real sign-in if you're handling sensitive buyer
information — they just keep casual visitors from stumbling onto the page.
