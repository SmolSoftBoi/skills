# Domain Map

Source pages:

- https://developers.pinterest.com/docs/api/v5/introduction/
- https://developers.pinterest.com/docs/api/v5/pins/
- https://developers.pinterest.com/docs/api/v5/boards/
- https://developers.pinterest.com/docs/api/v5/media/
- https://developers.pinterest.com/docs/api/v5/user_account/
- https://developers.pinterest.com/docs/api/v5/ad_accounts/
- https://developers.pinterest.com/docs/api/v5/campaigns/
- https://developers.pinterest.com/docs/api/v5/ad_groups/
- https://developers.pinterest.com/docs/api/v5/ads/
- https://developers.pinterest.com/docs/api/v5/reports/
- https://developers.pinterest.com/docs/api/v5/catalogs/
- https://developers.pinterest.com/docs/api/v5/feeds/
- https://developers.pinterest.com/docs/api/v5/product_groups/
- https://developers.pinterest.com/docs/api/v5/items/
- https://developers.pinterest.com/docs/api/v5/conversion_events/
- https://developers.pinterest.com/docs/api/v5/conversion_tags/

## Route by user intent

| Domain | Use when the user asks for | Main API families | Notes |
| --- | --- | --- | --- |
| Platform setup | App registration, OAuth, scopes, access tiers, token exchange | `oauth`, app setup docs | Solve setup issues before discussing endpoint details. |
| Organic content and users | Pins, boards, media uploads, basic user-account data | `pins`, `boards`, `media`, `user_account` | Default to raw REST and `curl`. |
| Ads and analytics | Ad accounts, campaigns, ad groups, ads, targeting, paid reporting | `ad_accounts`, `campaigns`, `ad_groups`, `ads`, `reports`, `keywords` | This is the main area where the Python SDK is useful. |
| Shopping | Catalogues, feeds, product groups, item ingestion, item diagnostics | `catalogs`, `feeds`, `product_groups`, `items` | Check sandbox support carefully before promising test coverage. |
| Conversions | Conversion events, conversion tags, cleanup requests | `conversion_events`, `conversion_tags`, related conversion endpoints | Keep auth and scope checks tight. Server-side conversion events use the conversion-token path; other conversion endpoints follow their own documented auth model. |

## Routing tips

- If the user says "Pins", "boards", "media upload", or "profile data", start in the organic domain.
- If the user says "campaign", "ad group", "creative", "audience", "keyword", "budget", or "report", start in ads and analytics.
- If the user says "catalogue", "feed", "merchant", "product group", or "items", start in shopping.
- If the user says "tag", "event", "conversion", or "attribution", start in conversions.
- If the user is sending server-side conversion events to `POST /ad_accounts/{ad_account_id}/events`, start by checking the conversion token rather than redirect URIs.
- If the user asks for "analytics", distinguish organic vs paid before choosing endpoints. Paid delivery analytics sit with ads families and `reports`.

## Python SDK rule

- Prefer the official Python SDK only for ads workflows or explicit Python requests.
- The current Pinterest SDK docs describe support for campaign management, ad groups, ads, keywords, customer lists, and audiences.
- Do not route non-ads requests to the SDK by default. Use raw REST unless the user requests a Python implementation and the SDK clearly covers the task.
