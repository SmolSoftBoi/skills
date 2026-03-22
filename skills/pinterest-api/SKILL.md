---
name: pinterest-api
description: Use this skill when the user needs to plan, implement, debug, or review a Pinterest API integration, including app registration, OAuth scopes or tokens, Pins and boards, ads and analytics, catalogues and feeds, conversions, sandbox testing, token debugging, Postman, or Pinterest quickstart tooling.
---

## Overview
- Use official Pinterest documentation first.
- The docs site is JavaScript-driven, so prefer a real browser when a plain fetch does not reveal navigation, endpoint details, or request examples.
- Default to raw REST and `curl` examples.
- Use the official Python SDK only when the user explicitly wants Python or when the task is centered on ad campaign management.
- Base claims only on official Pinterest documentation and any user-provided integration details available in the current workflow.
- If live documentation lookup is empty, incomplete, or inconsistent, retry with a browser or an alternative docs-navigation strategy before concluding the docs do not specify the answer.

## Reference Files
- Read [references/auth-and-access.md](references/auth-and-access.md) for app setup, grant selection, token exchange, refresh, revoke, and common auth failures.
- Read [references/domain-map.md](references/domain-map.md) to route requests to organic, ads, shopping, or conversion endpoints.
- Read [references/testing-and-tools.md](references/testing-and-tools.md) for sandbox support, product-limited tokens, Token Debugger, quickstart tooling, and Postman guidance.

# Instructions
## Workflow
1. Classify the request as platform setup, organic content, ads and analytics, shopping, conversions, or debugging.
2. Confirm prerequisites before suggesting implementation details: app approval or access tier, app ID and secret, exact redirect URI match, token state, scopes, and production vs sandbox.
3. Choose the authentication path. Default to the authorization-code flow.
4. Use client credentials only when the endpoint and use case do not require user context.
5. Route to the smallest relevant endpoint family and provide a minimal request example instead of long endpoint lists.
6. Escalate to debugging tools when the likely failure is token expiry, wrong environment, redirect mismatch, missing scopes, or unsupported sandbox coverage.
7. If the user's intent is clear and the next step is reversible and low-risk, proceed without unnecessary clarification; ask only when missing information would materially change the guidance.

## Authentication Defaults
- Treat apps created on or after 25 September 2025 as using continuous refresh tokens by default.
- Do not assume legacy refresh-token behavior for newer apps.
- Keep scope requests narrow and matched to the endpoint family.
- Prefer live docs over memory for exact scope names and request fields.

# Response Rules
- Cite the live Pinterest documentation pages used for the answer.
- Attach citations to the specific claims, scope names, endpoint details, or behavior notes they support.
- Never fabricate citations, URLs, scope names, endpoints, or request fields.
- Keep examples small and ready to run.
- Prefer `curl` for neutral examples.
- Add Python SDK examples only for ads workflows or when the user explicitly requests Python.
- Call out when sandbox support differs from production.
- If the user is missing app approval or a valid token, resolve that first instead of speculating about endpoint behavior.
- Return only the guidance needed for the user's request; avoid long endpoint inventories unless explicitly asked.

# Reasoning and Verification
- Work step by step internally.
- Verify endpoint families, scope names, request fields, and environment assumptions against live documentation when needed.
- Before finalizing, check that the answer is grounded in current docs, cites the supporting pages used, and matches the user's environment assumptions.
- Prefer the smallest correct example that satisfies the request.

# Verbosity
- Default to concise, implementation-ready answers.
- For code examples, prefer clarity and direct usability.
- Avoid repeating the user's request.