# Auth and Access

Source pages:

- https://developers.pinterest.com/docs/getting-started/connect-app/
- https://developers.pinterest.com/docs/getting-started/set-up-authentication-and-authorization/
- https://developers.pinterest.com/docs/api/v5/introduction/
- https://developers.pinterest.com/docs/api/v5/oauth-conversion_token/
- https://raw.githubusercontent.com/pinterest/api-quickstart/main/README.md
- https://github.com/pinterest/api-description/releases/tag/v5.15.0

## Access prerequisites

- Start by confirming the user has a Pinterest business account, has accepted the developer terms, and has registered an app.
- Treat trial access or the required access tier as the prerequisite for the work at hand. Pinterest's quickstart allows a trial-access-first path before the app is fully connected for broader use.
- Once the app is connected, the `Manage` view in `My apps` exposes the App ID and App secret needed for real requests.
- Confirm the access tier before promising production behaviour. Trial access is enough for initial integration and sandbox testing, but not every production use case.

## Redirect URI rules

- Match `redirect_uri` exactly against the value registered in the app profile.
- Reject secondary redirects in the OAuth callback chain. Pinterest requires the configured redirect target itself to be the callback destination.
- Check redirect mismatches before debugging deeper auth issues.

## Grant selection

- Use the authorization-code flow by default for user-scoped work such as organic content, ads, analytics, shopping, and most conversion-related work on a user's behalf.
- Use the client-credentials flow only when the endpoint and use case do not require user context. Re-read the live auth guide before issuing a request on this path because it is the less common flow and Pinterest can change the exact request requirements.
- For server-side conversion events at `POST /ad_accounts/{ad_account_id}/events`, use the conversion-token path instead of the standard redirect-URI troubleshooting flow.
- Generate that token with `POST /oauth/conversion_token` using a valid Pinterest OAuth token that has `ads:write`.
- Keep this exception narrow. Other conversion endpoints should follow their own documented auth requirements.

## Scope selection

- Start from the smallest scope set that can satisfy the task.
- Confirmed scope examples in the current docs include `boards:read`, `pins:read`, `user_accounts:read`, `ads:read`, and `ads:write`.
- Verify exact scope names on the live endpoint docs before expanding beyond those examples.

## Token exchange and lifecycle

- Exchange codes at `POST https://api.pinterest.com/v5/oauth/token`.
- Use HTTP Basic authentication with `client_id:client_secret` as the credentials pair.
- For the authorization-code flow, the live docs currently show `grant_type=authorization_code` with `code` and `redirect_uri`.
- Pinterest documents a token revoke endpoint under the `oauth` family. Use it when the user needs to invalidate access cleanly.
- Treat `POST /oauth/token` as the continuous refresh path.
- For apps activated before 25 September 2025, set `continuous_refresh=true` when the token flow requires it.
- For apps activated on or after 25 September 2025, continuous refresh is automatic.
- Do not send users toward an `everlasting_refresh` or other legacy refresh-token path.

## Common auth failure checks

- Missing trial access, the required access tier, or app credentials after the app has been connected
- Wrong environment: sandbox token used against production or the reverse
- Expired or invalid token
- Missing or overly narrow scopes
- Redirect URI mismatch
- Missing `continuous_refresh=true` for an older app activation that still requires that request parameter
- Using a standard OAuth token for `POST /ad_accounts/{ad_account_id}/events` instead of a conversion token
