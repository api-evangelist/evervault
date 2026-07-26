---
name: Create and use a network token
description: Create a network token to replace a PAN, generate a cryptogram for a transaction, and retrieve card art.
api: openapi/evervault-openapi-original.json
operations: [createNetworkToken, createNetworkTokenCryptogram, getNetworkToken, getCardArt]
---

# Create and use a network token

Use this skill to replace stored card numbers (PANs) with updatable network tokens that improve authorization rates and reduce fraud.

## Auth
HTTP Basic (App ID + API Key). See `authentication/evervault-authentication.yml`.

## Steps
1. **Create the token** — `POST /payments/network-tokens` (`createNetworkToken`) with the card details. Returns a `NetworkToken`.
2. **Generate a cryptogram** — `POST /payments/network-tokens/{network_token_id}/cryptograms` (`createNetworkTokenCryptogram`) at transaction time to produce a single-use cryptogram for the processor.
3. **Retrieve** — `GET /payments/network-tokens/{network_token_id}` (`getNetworkToken`) to fetch current token state; `GET .../card-art` (`getCardArt`) for issuer card art.
4. **Test** — use `POST /payments/network-tokens/{network_token_id}/simulate` (`simulateNetworkTokenUpdate`) in a Sandbox App to simulate an update; subscribe to the `payments.network-token.updated` webhook (`asyncapi/evervault-webhooks.yml`).

## Conventions
- RFC 9457 problem+json errors (`errors/evervault-problem-types.yml`).
- Evervault is PCI DSS Level 1 (`conformance/evervault-conformance.yml`); card data stays encrypted end to end.
