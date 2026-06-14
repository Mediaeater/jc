# Deploy / Hosting Notes

## Current setup
- **Source of truth:** this GitHub repo, branch **`master`** (path `/`).
- **Hosting:** GitHub Pages. Every push to `master` auto-builds and publishes.
- **Pages URL (working now):** https://mediaeater.github.io/jc/
- The site is self-contained — all images, video, the favicon, and `JohnnyCopollaBio.pdf` live in the repo and are referenced with relative paths. Only `og:image` / `og:url` meta tags use absolute URLs (correct for social sharing).

## To point www.johnnycoppola.com at this site (webmaster task)
The custom domain is **not** wired up yet. Today `johnnycoppola.com` resolves to an old
Apache host (`216.92.61.130`) serving a stale copy. To switch it to GitHub Pages:

1. **In this repo:** Settings → Pages → set **Custom domain** to `www.johnnycoppola.com`
   and Save (this commits a `CNAME` file). Enable **Enforce HTTPS** after DNS propagates.

2. **At the DNS registrar for johnnycoppola.com**, replace the current records:

   Apex `johnnycoppola.com` — four A records:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
   (Optional IPv6 AAAA: 2606:50c0:8000::153, :8001::153, :8002::153, :8003::153)

   Subdomain `www` — CNAME:
   ```
   www  CNAME  mediaeater.github.io
   ```

3. Remove/replace the old A record pointing to `216.92.61.130`.

DNS can take up to ~24h to propagate. Once it does, the GitHub Pages "DNS check"
in Settings → Pages will go green and HTTPS can be enforced.

## Updating content
Edit `index.html`, commit, and push to `master`. The site rebuilds in ~1 minute.
The next show date appears in two spots in `index.html` (the hero "Next Performance"
card and the show-section heading) plus the OpenTable reservation link.
