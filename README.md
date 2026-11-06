# guava.zip

The website for Guava, the smarter Finder for macOS: a static site served by Cloudflare Pages (same setup as guava.ventures). There is no build step; every file here is published as is.

- `index.html`: the homepage
- `download/`: download page and install steps; the app itself goes at `download/Guava.dmg`
- `help/`: the help page the app opens from Help › Guava Help (`https://guava.zip/help`)
- `privacy/`, `terms/`: policy pages (drafts; fill in the [BRACKETS])
- `404.html`: shown for unknown addresses
- `_headers`, `_redirects`: Cloudflare Pages settings (the DMG downloads as a file; `/dmg` and `/support` are short links)

## Publishing a new version of the app

On the Mac, in the app's folder (`~/guava`):

```bash
./scripts/make-dmg.sh                       # makes build/Guava.dmg
cp build/Guava.dmg ~/guava-zip/download/Guava.dmg
cd ~/guava-zip && git add download/Guava.dmg && git commit -m "Guava vX.Y" && git push
```

Cloudflare Pages redeploys on every push to `main`. Pages allows files up to 25 MB; if the DMG grows past that, attach it to a GitHub Release instead and point `/dmg` in `_redirects` at the release URL.

## Hosting setup (one time)

1. Cloudflare dashboard › Workers & Pages › Create › Pages › Connect to Git › pick this repo. Framework: None, build command: empty, output directory: `/`.
2. In the new project › Custom domains › add `guava.zip` and `www.guava.zip`. If the domain's DNS is on Cloudflare the records are created for you; otherwise point the domain's nameservers at Cloudflare first.
