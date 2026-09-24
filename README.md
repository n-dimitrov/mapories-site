# mapories-site

The landing page of [maporiesbooks.com](https://maporiesbooks.com), a static site on GitHub Pages. Issue: n-dimitrov/mapories-photobook#529.

- `index.html` — the page. It has no state: everything the owner or the price sheet decides comes from `site.json`, fetched fresh on every load. The HTML carries the current values, so a failed fetch changes nothing.
- `site.json` — `app_url` (where the app lives), `start_path` / `books_path`, the **start switch** (`start.enabled`, `notice`, `until`), product, price (a copy of the sheet, with `sheet_version`), `photo_floor`, `preview_time`, `ship_to` (ISO codes), `promotion`.
- `assets/`, `fonts/`, `wall/` — brand, the book's faces (self-hosted, no Google Fonts), the five cover prints.
- `CNAME` — the custom domain.

## Switching new books off

Edit `site.json`: `"start": {"enabled": false, "notice": "…", "until": "2026-10-02T09:00:00+02:00"}` and push. Every start button goes quiet and the notice shows the time in the visitor's zone. The app should refuse new books during the window on its own side too.

## Prices

The sheet in the app is the truth. `tools/sync_site.py --check --file ../mapories-site/site.json` in the app repo names any drift; without `--check` it rewrites the price block.

## Publishing

Push to `main`. Pages serves the root; a change is live within a minute or so (the page bypasses the CDN cache for `site.json`).
