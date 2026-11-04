# Spreadglass

Live: https://spreadglass.vercel.app/

A paper-only cross-venue market observatory. Real public BTC/USD, ETH/USD and SOL/USD depth from Kraken and Bitstamp. Original animated venue network, depth bars, cost controls, delayed hypothetical fills, prefunded paper inventories, execution tape and CSV export.

No accounts, API keys, deposits, orders or real money. No invented P&L history. Negative paper trades are allowed so costs are not hidden. Connect explicitly to request prices. Pause stops automatic refresh; books expire after20seconds.

## Honest execution model

Both venues trade the same asset against USD. No USD/USDT parity assumption. A quantity is fixed at decision time from selected buy-leg notional. After10–60seconds, new public depth must have been fetched after that deadline. Insufficient depth, stale books, outages or insufficient local fake balances reject the entire pair. Both legs settle atomically in this model, not on an exchange.

Costs: walk up to25Kraken levels /50Bitstamp levels; apply editable adverse slippage and a fee to each leg. Defaults40bps fee +2bps adverse slippage per leg are illustrative assumptions, not a current account quote. Venue fees vary by product/tier. Check the current official schedules yourself. The displayed P&L is cumulative execution spread minus costs, not portfolio mark-to-market. Held inventory price risk and rebalancing costs are excluded.

Real asynchronous quotes, partial fills, queue position, two-leg execution risk, transfer/withdrawal delays, borrow costs, taxes, rebalancing and regional eligibility prevent this from being an executable strategy or performance claim. The sphere is an original illustrative visualization, not a global scan. Exactly3assets and2venues are monitored. No profit guarantee, investment advice or automation of real trades.

## Data and reliability

Fixed allowlisted GET-only proxy with7second upstream timeout,10second per-instance cache and concurrent-request coalescing. Six reads per15second cycle, only after Connect and while visible; no hidden-tab auto refresh. Bitstamp source snapshot age is checked. Kraken REST offers level timestamps, not a whole-book timestamp: fetch age cannot prove source freshness. No WebSocket or millisecond execution claim.

No arbitrary URLs, credentials, personal data, external scripts or cross-origin browser requests. Session data stays in memory and disappears on reload. The tape and chart retain up to1,000entries/samples; CSV exports the retained tape. Providers and host see requests/IP metadata. In-memory limits are not a globally enforced rate limiter. Public-provider terms, availability and host free-tier quotas may change; the service can fail closed rather than insert substitutes. No durable queue is needed: pending paper pairs are in-memory, serialized and cancelled by reset/reload. No retry storm; normal15second cycles can try unavailable feeds again. This is a personal/non-commercial educational demonstration, not a market-data redistribution service.

## Sources

- Kraken public REST depth: https://docs.kraken.com/api/docs/rest-api/get-order-book/
- Kraken protocol alternative, not used: https://docs.kraken.com/exchange/api-reference/spot-websocket-v2/book
- Kraken fee schedule: https://www.kraken.com/features/fee-schedule
- Bitstamp public order-book API and limits: https://www.bitstamp.net/api/
- Bitstamp fees: https://www.bitstamp.net/fee-schedule/

Source docs checked4November2026. Some services can block regions. Coinbase returned403 in this environment and is not used. These are public prices, not access to exchange accounts.

## Verification

Model tests cover depth integration, cost arithmetic, inventory conservation, missing/crossed/stale books and insufficient balances. Proxy tests check fixed market allowlist, GET-only behavior, cache and concurrent coalescing. Browser tests separate real feed loading from clearly intercepted failure fixtures. No test fixture or seeded book ships into the app. Repository identity is Aditya2375; commit descriptions are empty.
