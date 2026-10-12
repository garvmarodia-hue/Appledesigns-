# Original security prompts

Source: [Secure Your AI / Vibe-Coded App](https://claude.ai/public/artifacts/6a016c9b-c858-471a-8c5e-639796d64874). The six prompts below preserve the artifact wording. They are reference material; the skill entry point defines scope and verification.

## 1. Secure Authentication

Act as a senior security engineer. Review the authentication system of this project and make it secure. Ensure passwords are securely hashed, sessions expire, email verification is enabled, password reset tokens expire, login attempts are rate limited, and authentication secrets are never exposed to the frontend. Refactor any insecure authentication logic.

## 2. Prevent Unauthorized Data Access

Review all API endpoints and database queries. Ensure every request verifies the logged-in user owns the data being accessed. Prevent insecure direct object reference (IDOR) vulnerabilities by enforcing ownership checks before reading, modifying, or deleting any resource.

## 3. Secure Deployment & Monitoring

Configure the application for secure deployment. Enforce HTTPS, ensure secrets are stored securely, restrict direct database access from the public internet, and add logging for authentication attempts, API errors, and unusual traffic patterns so suspicious behavior can be detected.

## 4. Prevent Abuse & Bot Attacks

Add abuse protection to the application. Implement rate limiting for login attempts, API endpoints, account creation, and AI generation requests. Prevent bots or automated scripts from repeatedly calling endpoints or scraping data.

## 5. Protect Secrets & API Keys

Scan the entire project for secrets and credentials. Ensure API keys, database service keys, and tokens are never exposed in frontend code or committed to the repository. Move all secrets to secure environment variables and ensure they are only used on the server.

## 6. Validate & Sanitize User Input

Identify every place where user input enters the system including forms, APIs, uploads, and query parameters. Add strict validation and sanitization to prevent SQL injection, command injection, script injection, and unsafe file uploads. Reject invalid data and enforce strict input types.

