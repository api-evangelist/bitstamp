# Bitstamp

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
