# Renald Salin — Links

A mobile-first link hub. Installs to the home screen on iOS and Android, works
offline, and generates its own QR code.

```
index.html              the page + your profile config
manifest.webmanifest    PWA metadata
sw.js                   offline cache
icons/                  home screen icons
.nojekyll               stops GitHub Pages mangling the files
```

---

## Adding your profile photo

1. Save your photo into this folder as `photo.jpg` (a square crop around
   512×512 is plenty — anything over ~300 KB just slows the page down).
2. Open `index.html` and set the `photo` line:

   ```js
   photo: "photo.jpg",
   ```

3. Commit and push. Leave it as `""` and you get the **RS** monogram instead.

The photo can also be a full URL (`https://…/me.jpg`) if you host it elsewhere.

---

## Adding your links

Everything you edit lives in one block near the bottom of `index.html`, marked
`YOUR PROFILE`:

```js
const PROFILE = {
  name: "Renald Salin",
  tagline: "UI/UX Designer at Shore360",
  photo: "photo.jpg",
  links: [
    { platform: "linkedin",  url: "https://linkedin.com/in/your-handle" },
    { platform: "instagram", url: "https://instagram.com/your-handle" },
    { platform: "facebook",  url: "https://facebook.com/your-handle" },
    { platform: "website",   url: "renaldsalin.com" }
  ]
};
```

- Leave a `url` as `""` and that row shows greyed out as "Not set yet".
- `https://` is added for you if you leave it off.
- For `email`, just write the address — `mailto:` is added for you.
- Reorder the rows by reordering the array. Delete a line to drop a platform.

Available platforms: `linkedin` `instagram` `facebook` `x` `threads` `tiktok`
`youtube` `behance` `dribbble` `github` `whatsapp` `email` `website`

---

## Publishing to GitHub Pages

One-time setup:

```bash
git init
git add .
git commit -m "Add links page"
git branch -M main
git remote add origin https://github.com/<your-username>/links.git
git push -u origin main
```

Then in the repo on github.com: **Settings → Pages → Source: Deploy from a
branch → Branch: `main`, folder: `/ (root)` → Save.**

A minute later it's live at `https://<your-username>.github.io/links/`.

Every change after that is just:

```bash
git add . ; git commit -m "Update links" ; git push
```

### After you change index.html

Bump the cache name in `sw.js` so phones that already installed the page pick
up the new version instead of serving the cached one:

```js
const CACHE = "rs-links-v2";   // v1 -> v2
```

---

## Your QR code

Open the live page on any device, tap **QR code**, then **Save PNG**. The code
encodes whatever URL the page is served from, so generate it *after* the site
is live — and regenerate it if you later move to a custom domain.

## Custom domain (optional)

Add a file named `CNAME` containing just your domain, e.g.
`links.renaldsalin.com`, point a CNAME DNS record at
`<your-username>.github.io`, then set the domain under Settings → Pages. Worth
doing before printing the QR anywhere, since it's the one change that would
otherwise invalidate the code.
