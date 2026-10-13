# maporiesbooks.com

The landing page of Mapories Books, served as a static site.

- `index.html` — the page.
- `site.json` — the page's settings: where the app lives, whether new books can be started, the price and the countries shipped to.
- `assets/`, `fonts/`, `wall/` — brand, self-hosted fonts, the cover prints.

## Link preview image

`assets/og-image.png` (1200×630) is rendered from `tools/og-card.html`, which copies the
hero cover markup and styles out of `index.html`. After changing the hero cover, rebuild it
with headless Chrome and bump the `?v=` on the two `og:image` / `twitter:image` tags so
Teams, Slack and LinkedIn refetch it:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu \
      --hide-scrollbars --window-size=1200,630 --virtual-time-budget=4000 \
      --screenshot="$PWD/assets/og-image.png" "file://$PWD/tools/og-card.html"
