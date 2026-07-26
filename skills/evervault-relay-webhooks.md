---
name: Configure a Relay and subscribe to webhooks
description: Create an Evervault Relay to encrypt/decrypt data in transit and register a webhook endpoint to receive events.
api: openapi/evervault-openapi-original.json
operations: [createRelay, listRelays, createWebhookEndpoint, listWebhookEndpoints]
---

# Configure a Relay and subscribe to webhooks

Use this skill to stand up a Relay (an encrypting/decrypting proxy) and receive real-time event notifications.

## Auth
HTTP Basic (App ID + API Key). See `authentication/evervault-authentication.yml`.

## Steps
1. **Create a Relay** — `POST /relays` (`createRelay`) with the destination and route actions (encrypt/decrypt rules, JSONPath field selection). Returns a `Relay`.
2. **List / verify** — `GET /relays` (`listRelays`) to confirm the Relay, or `GET /relays/{id}` (`fetchRelay`).
3. **Add a custom domain** (optional) — `POST /relays/{relay_id}/custom-domains` (`createCustomDomain`).
4. **Subscribe to events** — `POST /webhook-endpoints` (`createWebhookEndpoint`) with your URL and the event types (e.g. `payments.3ds-session.success`, `payments.card.updated`). List with `GET /webhook-endpoints` (`listWebhookEndpoints`).

## Conventions
- Event catalog: `asyncapi/evervault-webhooks.yml`.
- RFC 9457 problem+json errors (`errors/evervault-problem-types.yml`).
