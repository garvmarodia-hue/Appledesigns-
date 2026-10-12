---
name: ai-app-security
description: Review and improve app security before launch using six checks for authentication, authorization, deployment, abuse protection, secrets, and input handling. Use when the user asks to secure an AI-built or other web app, review security, or perform a pre-launch security check.
---

# AI App Security

Adapted from the shared [Secure Your AI / Vibe-Coded App guide](https://claude.ai/public/artifacts/6a016c9b-c858-471a-8c5e-639796d64874). The [six original prompts](references/original-prompts.md) are preserved as reference material. Use the checks below to produce evidence-backed findings and, when requested, concrete fixes.

## Establish the scope

Inspect the repository instructions and identify the app's framework, authentication provider, API routes, data store, deployment configuration, and AI generation endpoints. Follow existing provider integrations rather than adding a second authentication system. Review the relevant code and configuration before proposing changes.

Treat a review request as a review; implement fixes when the user asks to secure or fix the app. Work on code and local test fixtures within the authorized project. Change live deployment settings or credentials only within the user's authorized scope. When production configuration cannot be inspected, record the gap rather than inferring that it is secure.

## Apply the six checks

1. **Authentication.** Trace signup, login, session validation, logout, email verification, and password reset where applicable. Check password hashing or managed-provider handling, session expiration, cookie security, expiring single-use reset tokens, and login throttling. Check provider configuration before calling a missing custom implementation a vulnerability. If login is not part of the product, record this check as not applicable.

2. **Authorization and data ownership.** Trace reads, writes, and deletes from the endpoint to the database. Verify access on the server for the actual user's role, tenant, and resource ownership; do not rely on hidden buttons or user-supplied owner IDs. Include shared resources, privileged actions, list queries, and bulk operations. For a data API exposed to clients, check its access policies as well as server-side checks.

3. **Deployment and monitoring.** Inspect HTTPS enforcement, secret storage, database access controls, production error handling, and useful authentication and API logs. Distinguish a protected public data API from unrestricted database access. Redact credentials, session tokens, and private payloads from logs. Check how unusual traffic and repeated failures become visible to the operator.

4. **Abuse protection.** Check login, signup, costly API calls, uploads, and AI generation for rate and resource limits appropriate to the app. Verify that enforcement survives multiple processes or instances, and that direct API calls cannot bypass client controls. For AI requests, inspect request size, concurrency, output/token budgets, and any existing per-user usage limits. Choose thresholds from product needs rather than inventing a universal limit.

5. **Secrets and API keys.** Inspect relevant source, environment configuration, generated client assets, and deployment settings without printing secret values. Distinguish intentionally public client identifiers from confidential credentials. Keep privileged keys and provider secrets server-side. If a credential was exposed, moving it to an environment variable does not revoke the old credential; report the exposure and the required rotation. Do not rewrite repository history as a routine fix.

6. **Input handling.** Trace forms, API bodies, query parameters, path values, and uploads. Use server-side schemas, type and size limits, parameterized queries, context-appropriate output encoding, and safe process APIs. Treat rich HTML and file uploads according to their actual risks. Avoid blanket string replacements that corrupt valid data or create false confidence. Confirm invalid input is rejected before expensive or privileged work.

## Verify meaningful behavior

For each material fix, reproduce the issue or add a focused regression check. Use local fixtures to demonstrate the relevant boundary: unauthenticated and cross-user requests are rejected, permitted users still work, expired or reused reset tokens fail, limits are enforced, malformed inputs are rejected, and confidential values do not enter client output. Test only flows affected by the change, then run required project checks.

Do not call a check passed merely because a file contains a security setting. Separate code review evidence, executed tests, and unverified deployment assumptions. Do not probe unrelated services or create live traffic for a code-only review.

## Deliver findings or fixes

Lead with the most consequential issue and its concrete trigger. Provide a compact result for all six checks using **verified**, **issue found**, **not applicable**, or **not verified**, with supporting file locations or test results. For issues, explain the impact and the specific fix; prioritize by actual exploitability and impact.

If changes were made, explain what changed, the behavior tested, and any remaining launch blockers. Keep secret values out of findings, commits, screenshots, and downloadable reports. These six checks are a scoped pre-launch review; do not claim the app is secure solely because the checklist is complete.
