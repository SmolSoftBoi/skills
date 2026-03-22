# Testing and Tools

Source pages:

- https://developers.pinterest.com/docs/developer-tools/quickstart-tools/
- https://developers.pinterest.com/docs/developer-tools/sandbox/
- https://developers.pinterest.com/docs/developer-tools/token-debugger/
- https://developers.pinterest.com/docs/api/v5/oauth-conversion_token/
- https://github.com/pinterest/api-quickstart#readme

## Fast test paths

- Use a product-limited token when the user wants to smoke-test basic organic reads without building a full OAuth flow first.
- The current docs state that product-limited tokens cover `pins:read`, `boards:read`, and `user_accounts:read`.
- Use a sandbox token when the user needs broader scope coverage in the sandbox environment only.

## Sandbox guidance

- Treat sandbox as a separate environment, not a safe copy of production.
- Re-check the current sandbox support list before promising coverage. The docs note that this list is updated periodically.
- The current sandbox page shows support across many endpoint families, including pins and boards, media, user accounts, campaign management, labels, keywords, OAuth, resources, terms, and key shopping endpoints such as catalogues, feeds, product groups, and items.
- Call out any gap between the endpoint the user wants and the endpoints Pinterest currently lists as sandbox-compatible.

## Token Debugger

- Use the Token Debugger when the likely problem is expiry, invalid tokens, wrong scopes, or a user session issue.
- The current docs say the debugger accepts Pinterest OAuth access or refresh tokens for version 5, including the `pina` and `pinr` prefixes.
- Check environment, app ID, user ID, created time, expiry, login state, and scopes before changing code.
- For server-side conversion events, first confirm the integration generated a dedicated conversion token via `POST /oauth/conversion_token` instead of reusing a standard OAuth token.

## Quickstart and Postman

- Use the official GitHub quickstart repo when the user needs working examples, environment setup hints, or a quick way to confirm that auth is wired correctly.
- Use the quickstart tools page when the user wants the Postman collection path or a faster way to test endpoints interactively.
- Prefer these tools for early integration proof, then reduce to the smallest reproducible `curl` command in the final answer.

## Debug order

1. Confirm the environment: production vs sandbox.
2. Confirm the token type and expiry.
3. Confirm the app has trial access or the required access tier.
4. For `POST /ad_accounts/{ad_account_id}/events`, confirm the caller is using a conversion token rather than a standard OAuth token.
5. Confirm scopes for the endpoint family.
6. Confirm the endpoint is supported in the chosen environment.
7. Retry with a minimal `curl` request before changing more code.
