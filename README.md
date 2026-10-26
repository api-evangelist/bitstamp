# Bitstamp

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Bitstamp is a European cryptocurrency exchange founded in 2011, offering REST and WebSocket APIs for spot trading, order management, market data, account balance inquiries, and transaction history across major crypto pairs including BTC, ETH, XRP, LTC, and many others.

**API Documentation:** https://www.bitstamp.net/api/

## APIs

- **REST API** — Public market data and authenticated private endpoints for trading and account management. Base URL: `https://www.bitstamp.net`
- **WebSocket API v2** — Real-time streaming of order book updates, live trades, ticker data, and private account events. Connection URL: `wss://ws.bitstamp.net`

## Authentication

Private REST endpoints require HMAC-SHA256 signature authentication using five mandatory headers:

- `X-Auth`: `BITSTAMP {api_key}`
- `X-Auth-Signature`: SHA256 HMAC of the request components
- `X-Auth-Nonce`: Unique 36-character lowercase string (valid for 150 seconds)
- `X-Auth-Timestamp`: UTC timestamp in milliseconds
- `X-Auth-Version`: `v2`

WebSocket private channels use tokens obtained via `POST /api/v2/websockets_token/`.

## Rate Limits

- 400 requests per second (standard)
- 10,000 requests per 10-minute window (default burst threshold)
- Custom limits available for institutional clients

## Key Endpoints

### Public (no auth required)
- `GET /api/v2/ticker/{market_symbol}/` — Current ticker
- `GET /api/v2/order_book/{market_symbol}/` — Order book
- `GET /api/v2/transactions/{market_symbol}/` — Recent transactions
- `GET /api/v2/ohlc/{market_symbol}/` — OHLC candlestick data
- `GET /api/v2/markets/` — All available markets
- `GET /api/v2/currencies/` — All supported currencies

### Private (auth required)
- `GET /api/v2/account_balances/` — Account balances
- `POST /api/v2/buy/{market_symbol}/` — Place buy order
- `POST /api/v2/sell/{market_symbol}/` — Place sell order
- `POST /api/v2/cancel_order/` — Cancel order
- `GET /api/v2/open_orders/all/` — List open orders
- `GET /api/v2/fees/trading/` — Trading fee schedule
- `POST /api/v2/revoke_all_api_keys/` — Kill-switch: revoke all API keys

## Fees

API access is free. Trading fees use a volume-based maker/taker model starting at 0.30% maker / 0.40% taker for volumes under $10,000/month, reducing to 0.00% maker / 0.03% taker for volumes over $20M/month.

## Links

- [API Documentation](https://www.bitstamp.net/api/)
- [Fee Schedule](https://www.bitstamp.net/fee_schedule/)
- [Status Page](https://status.bitstamp.net/)
- [Support](https://www.bitstamp.net/support/)
- [Institutional](https://www.bitstamp.net/institutional/)
