# skoddet.com

GitHub Pages **user site** (repo `jensnielsen-stack.github.io`), served under
the custom domain `https://skoddet.com/` via the `CNAME` file.

## Why this repo exists

Originally created to host `app-ads.txt` at a domain root — AdMob's crawler
looks for it at the root of whatever developer website an app declares on its
App Store listing, and nowhere else, so a *project* Pages site (which can't
serve anything at its own domain root) can't host it.

`jensnielsen-stack.github.io` itself turned out to be a second problem, not
just a naming inconvenience: `github.io` sits on the Public Suffix List (the
same mechanism that marks `.co.uk` as a real TLD boundary, not a subdomain of
`.uk`) precisely because arbitrary users each get their own `<name>.github.io`
site. AdMob's crawler rejected it as an "unsupported subdomain" even though
the file itself was byte-correct. `skoddet.com`, bought 2026-09-12
specifically to fix this, is an ordinary registered domain with no such
ambiguity.

It's also meant to grow into the umbrella site for every app in this
developer's portfolio, not just Space Tilters — one domain, one `app-ads.txt`,
with each app's own support page under a subpath (`skoddet.com/space-tilters/`
etc.), and the existing per-app Pages sites (like
[spacetilters-pages](https://github.com/jensnielsen-stack/spacetilters-pages))
migrated in over time rather than all at once.

## Contents

- `CNAME` — tells GitHub Pages to serve this repo under `skoddet.com` instead
  of (or as well as — see note below) `jensnielsen-stack.github.io`.
- `app-ads.txt` — authorized digital sellers for the apps. Every line names a
  seller permitted to sell this developer's ad inventory. **An `app-ads.txt`
  that exists but omits a network declares that network unauthorized**, so this
  file must list every ad network in use, or not exist at all.
- `index.html` — a minimal root page, so the domain root isn't a bare 404.

**Once DNS is pointed at GitHub Pages** (four A records at the registrar —
185.199.108.153, .109.153, .110.153, .111.153 — see GitHub's own docs),
`jensnielsen-stack.github.io` redirects to `skoddet.com` rather than serving
content directly; that's normal custom-domain behavior, not a bug.

## Verifying app-ads.txt

```bash
curl -sI https://skoddet.com/app-ads.txt | head -1
```

Expect `HTTP/2 200`. After that, update the App Store's Developer Website
field to `skoddet.com`, then AdMob → Apps → (app) → app-ads.txt → "Check for
updates". Google's crawl can lag by a day or two.
