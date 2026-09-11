# jensnielsen-stack.github.io

GitHub Pages **user site**, serving at the root of
`https://jensnielsen-stack.github.io/`.

## Why this repo exists

It exists to host `app-ads.txt` at the domain root.

Ad networks (AdMob and its demand partners) look for `app-ads.txt` at the root
of whatever developer website an app declares on its App Store listing — i.e.
`https://jensnielsen-stack.github.io/app-ads.txt`, and nowhere else. A file
served from a *project* site path such as
`https://jensnielsen-stack.github.io/spacetilters-pages/app-ads.txt` is never
fetched, because project sites can't serve anything at the domain root.

Only a user site repo — one named exactly `<username>.github.io` — can. Hence
this repo, separate from
[spacetilters-pages](https://github.com/jensnielsen-stack/spacetilters-pages),
which remains the actual Space Tilters site.

## Contents

- `app-ads.txt` — authorized digital sellers for the apps. Every line names a
  seller permitted to sell this developer's ad inventory. **An `app-ads.txt`
  that exists but omits a network declares that network unauthorized**, so this
  file must list every ad network in use, or not exist at all.
- `index.html` — a minimal root page, so the domain root isn't a bare 404.

## Verifying app-ads.txt

```bash
curl -sI https://jensnielsen-stack.github.io/app-ads.txt | head -1
```

Expect `HTTP/2 200`. After that, AdMob → Apps → (app) → app-ads.txt →
"Check for updates". Google's crawl can lag by a day or two.
