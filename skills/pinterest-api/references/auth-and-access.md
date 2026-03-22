# Auth and Access

Source pages:

- https://developers.pinterest.com/docs/getting-started/connect-app/
- https://developers.pinterest.com/docs/getting-started/set-up-authentication-and-authorization/
- https://developers.pinterest.com/docs/api/v5/introduction/

## Access prerequisites

- Start by confirming the user has a Pinterest business account, has accepted the developer terms, and has registered an app.
- Treat app approval as a hard prerequisite for real API work. The docs state approved apps expose the app ID and app secret in `My apps`.
- Confirm the access tier before promising production behaviour. Trial access is enough for initial integration and sandbox testing, but not every production use case.

## Redirect URI rules

- Match `redirect_uri` exactly against the value registered in the app profile.
- Reject secondary redirects in the OAuth callback chain. Pinterest requires the configured redirect target itself to be the callback destination.
- Check redirect mismatches before debugging deeper auth issues.

## Grant selection

- Use the authorisation-code flow by default for user-scoped work such as organic content, ads, analytics, shopping, and conversions on a user's behalf.
- Use the client-credentials flow only when the endpoint and use case do not require user context. Re-read the live auth guide before issuing a request on this path because it is the less common flow and Pinterest can change the exact request requirements.

## Scope selection

- Start from the smallest scope set that can satisfy the task.
- Confirmed scope examples in the current docs include `boards:read`, `pins:read`, `user_accounts:read`, `ads:read`, and `ads:write`.
- Verify exact scope names on the live endpoint docs before expanding beyond those examples.

## Token exchange and lifecycle

- Exchange codes at `POST https://api.pinterest.com/v5/oauth/token`.
- Use HTTP Basic authentication with `client_id:client_secret` as the credentials pair.
- For the authorisation-code flow, the live docs currently show `grant_type=authorization_code` with `code` and `redirect_uri`.
- Pinterest documents a token revoke endpoint under the `oauth` family. Use it when the user needs to invalidate access cleanly.
- For apps created on or after 25 September 2025, assume continuous refresh tokens by default. The docs call out older refresh-token behaviour only for apps created before that date.

## Common auth failure checks

- App not approved or app secret missing in `My apps`
- Wrong environment: sandbox token used against production or the reverse
- Expired or invalid token
- Missing or overly narrow scopes
- Redirect URI mismatch
- Integration built around the legacy refresh model instead of the continuous refresh model
