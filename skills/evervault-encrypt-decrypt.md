---
name: Encrypt and decrypt data with Evervault
description: Encrypt sensitive JSON or file data with Evervault, inspect encrypted values, and decrypt them server-side.
api: openapi/evervault-openapi-original.json
operations: [encrypt, inspect, decrypt]
---

# Encrypt and decrypt data with Evervault

Use this skill to protect sensitive data with Evervault's encryption model, where Evervault holds the keys and you hold the ciphertext.

## Auth
Server-side calls use HTTP Basic auth: username = App ID, password = API Key (send `Authorization: Basic base64(app_id:api_key)`). See `authentication/evervault-authentication.yml`.

## Steps
1. **Encrypt** — `POST /encrypt` (`encrypt`) with the JSON object or file payload. Evervault returns the data with sensitive fields replaced by encrypted strings. Store the ciphertext in your own database.
2. **Inspect** (optional) — `POST /inspect` (`inspect`) to retrieve metadata about encrypted values without decrypting them.
3. **Decrypt** — `POST /decrypt` (`decrypt`) with the encrypted payload when you need plaintext server-side. Consider running decryption inside a Function (`createFunctionRun`) so plaintext never touches your infrastructure.

## Conventions
- Errors are `application/problem+json` (RFC 9457) with `code`/`title`/`status`/`detail` — see `errors/evervault-problem-types.yml`.
- Test safely in a Sandbox App (`sandbox/evervault-sandbox.yml`); sandbox-encrypted data only decrypts with the same sandbox app key.
