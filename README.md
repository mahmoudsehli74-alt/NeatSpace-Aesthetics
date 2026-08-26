# NeatSpace-Aesthetics — Bridge Storefront

Warm-minimal Scandinavian landing storefront for the **NeatSpace Aesthetics**
Pinterest account. GitHub Pages + client-side hydration from per-product JSON
committed by NeatSpace-Core's bridge (`pinner/tools/bridge.py`).

## Handshake

`/?id=<product_key>` → fetch `./products/<product_key>.json` → hydrate.

The normalizer in `app.js` accepts **both** payload generations:

- **A — bridge canonical (nested)**, as committed by `_landing_payload` today:
  `{key, title, description, hashtags[], landing_angle, product:{price:{current,original,currency}, image, images[]}, affiliate_url, disclosure}`
- **B — flat schema**: `{id, title, description, landing_angle, price, original_price, affiliate_url, images[]}`

Prices may be numbers or strings ("$149.00", "US $149"). Unknown fields are
ignored; a missing affiliate URL disables the CTA instead of dead-linking.

## Files

| File | Purpose |
|---|---|
| `index.html` | Semantic skeleton / product / fallback views |
| `style.css` | Warm Scandi theme, 4:5 editorial gallery, sticky CTA, ≥720px two-column |
| `app.js` | Sanitizer, dual-shape normalizer, fetch/hydrate, carousel, 404 grid |
| `featured.json` *(optional)* | Up to 6 product keys for the fallback page |

## Security posture

Untrusted marketplace text renders via `textContent`/`createElement` only
(no `innerHTML`, no eval); the `?id` param is whitelisted to
`[A-Za-z0-9._-]{1,120}`; images carry `referrerpolicy="no-referrer"`; CTAs are
`rel="nofollow sponsored noopener"`.

## Deploy

Push to `main`, enable Pages (branch: main, root). Custom domain goes both in
Pages settings and Atlas `accounts.site.custom_domain`.
